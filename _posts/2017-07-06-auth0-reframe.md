---
layout: post
title: Wiring Auth0 Lock to re-frame
---

Quick one: I'm working on an app using [re-frame][re-frame] framework,
which uses [reagent][reagent], itself a ClojureScript wrapper of Facebook's [ReactJS][react].

[re-frame]: https://github.com/Day8/re-frame
[reagent]:  https://github.com/reagent-project/reagent
[react]:    https://facebook.github.io/react/

One of the earlier tasks is to wire the app up to Auth0, an IaaS, and for simplicity, I'm
using their [Lock][lock] library.

[lock]: https://auth0.com/docs/libraries/lock/v10

## Effect handler code

````clojure
(ns your-app.auth0
  (:require [re-frame.core :as re-frame]
            [cljsjs.auth0-lock]))

(defonce lock-instance (atom nil))

(defn *js->clj
  [js]
  (js->clj js :keywordize-keys true))

(defn make-lock
  [client-id domain options on-authenticated]
  (let [lock (js/Auth0Lock. client-id domain
                            (clj->js options))]
    (.on lock "authenticated"
         #(re-frame/dispatch (conj on-authenticated (*js->clj %))))
    lock))

(defn get-user-info
  [lock value]
  (.getUserInfo
   lock (:access-token value)
   (fn [e p]
     (let [error   (*js->clj e)
           profile (*js->clj p)]
       (if e
         (re-frame/dispatch (conj (:on-failure value) error))
         (re-frame/dispatch (conj (:on-success value) profile)))))))

(re-frame/reg-fx
 :lock
 (fn [value]
   (let [lock @lock-instance]
     (case (:method value)
       :instantiate   (reset! lock-instance
                              (make-lock (:client-id value)
                                         (:domain value)
                                         (:options value)
                                         (:on-authenticated value)))
       :show          (.show lock)
       :logout        (.logout lock
                               (clj->js {:returnTo (:return-to value)}))
       :get-user-info (get-user-info lock value)
       nil))))

````

### Event handler code

On app-startup (called with a `dispatch-sync`)


````clojure
(re-frame/reg-event-fx
 :initialize-lock
 (fn [_ _]
   {:lock {:method           :instantiate
           :client-id        config/auth0-client-id
           :domain           config/auth0-domain
           :options          lock-options
           :on-authenticated [:new-auth-result]}}))
````

Log in

````clojure
(re-frame/reg-event-fx
 :login
 (fn [_ _]
   {:lock {:method :show}}))
````

On Auth result

````clojure
(re-frame/reg-event-fx
 :new-auth-result
 (fn [{:keys [db]}
      [_ {new-access-token :accessToken
          new-id-token     :idToken}]]
   {:db          (assoc db
                        :id-token new-id-token
                        :access-token new-access-token)
    :lock        {:method :get-user-info
                  :access-token new-access-token
                  :on-success [:profile-change]
                  :on-failure [:auth-fail]}}))
````

etc.

## Thoughts

We are not using the `app-db` to store the lock object. But this kind of lives
in a separate world anyways.

This followed the pattern set by [re-frame-http-fx][http-fx], callbacks via
dispatches and all.

[http-fx]: https://github.com/Day8/re-frame-http-fx

Setting the behaviour of the lock object via the `on` call on creation feels
more appropriate than exposing the `on` method directly. We are limiting that
stateful behaviour to app setup, when we can impose more control on sequence of
events.

If we have a relatively simple auth flow, doing things in this re-frame purist
way doesn't add a whole lot more value, as compared to triggering it via
side-effects, but it might allow for more complex events.

It might be worth fleshing this out into a full (micro)library. re-auth0-fx?
