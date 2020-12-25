# Migrate LocalStorage

This plugin can be used to persist LocalStorage data when migrating from `UIWebView` to `WKWebView`. It is compatible with cordova-ios@6.x. All related
files will be copied over automatically during startup so the user can simply pick up where they
left of.

## How to use

Simply add the plugin to your cordova project via the cli:
```sh
cordova plugin add https://github.com/harupiie/cordova-plugin-migrate-localstorage
```

If you have any custom scheme set in the config.xml. You will have to change the https://github.com/khatridev/cordova-plugin-migrate-localstorage/blob/d22b39728451661d3d41eaa853258e07b96e1b4b/src/ios/MigrateLocalStorage.m#L52 . [ By default, set for app://localhost scheme ]

## Notes

- LocalStorage files are only copied over once and only if no LocalStorage data exists for `WKWebView`
yet. This means that if you've run your app with `WKWebView` before this plugin will likely not work.
To test if data is migrated over correctly:
    1. Install the app with version lower than cordova-ios@6.x 
    2. Run your app and store some data in LocalStorage
    3. Add the plugin
    4. Run your app again. Your data should still be there!

- Once the data is copied over, it is not being synced back to `UIWebView` so any changes done in
`WKWebView` will not persist should you ever move back to `UIWebView`. If you have a problem with this,
let us know in the issues section!

## Background

One of the drawbacks of migrating Cordova apps to `WKWebView` is that LocalStorage data does
not persist between the two. Unfortunately,
[cordova-plugin-wkwebview-engine](https://github.com/apache/cordova-plugin-wkwebview-engine)
does not offer a solution for this out of the box (see
https://issues.apache.org/jira/browse/CB-11974?jql=project%20%3D%20CB%20AND%20labels%20%3D%20wkwebview-known-issues).
