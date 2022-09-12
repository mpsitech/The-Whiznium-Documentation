[back](./README.md)

# Setting Up The Vue.js CLI For Use With Whiznium StarterKit

The following instructions have been tested on a Linux workstation running ubuntu 20.04.

## Development

In the development phase, it is advisable to use the Vue.js CLI along with Webpack, which provides live updates of served content as the Vue.js code is being changed.

- prepare a new Vue.js project within the Whiznium folder structure
```
cd ${WHIZROOT}/web
vue create vueappwzsk
```

- select __Default ([Vue 2] babel, eslint)__

- continue by adding dependencies
```
cd vueappwzsk
npm install axios@0.21.4
npm install vue-axios@3.4.0
npm install vue-cli-plugin-axios@0.0.4
npm install vuetify@2.6.1
vue add axios
vue add vuetify
```

- select __Default (recommended)__

- start the development server
```
npm run serve
```

By navigating to http://127.0.0.1:8080, e.g. in Chrome, it can be verified that the project setup has completed successfully.

The further steps prepare the Whiznium StarterKit _combined engine_ for interaction with the actual Whiznium StarterKit Vue.js app.

- overwrite the default Vuetify.js app
```
cd ${WHIZNIUM_DEV}/rep/wzsk/_rls/vueappwzsk_any
./checkout.sh
```

- edit the preferences file ``${WHIZROOT}/bin/wzskcmbd/PrefWzskcmbd.xml`` to allow for cross-site scripting. This is accomplished by inserting ``http://127.0.0.1:8080`` in the ``<StgWzskAppsrv.cors>`` setting

- in a separate terminal, run ``Wzskcmbd`` from the command line
```
cd ${WHIZROOT}/bin/wzskcmbd
./Wzskcmbd
```

Now, Chrome should show the the Whiznium StarterKit Vue.js app when navigating to http://127.0.0.1:8080.

## Deployment

For deployment, Webpack transpilation is required:

- modify ``${WHIZROOT}/web/vueappwzsk/vue.config.js`` so that the ``module.exports`` section reads
```
module.exports = {
  publicPath: '/web/',
  transpileDependencies: [
    'vuetify'
  ]
}
```

- run ``npm run build`` which places its results in the ``dist`` sub-folder

- quit ``Wzskcmbd``

- edit the preferences file ``${WHIZROOT}/bin/wzskcmbd/PrefWzskcmbd.xml`` by setting ``<StgWzskPath.webpath>`` to ``${WHIZROOT}/web/vueappwzsk/dist`` where ``${WHIZROOT}`` has to be replaced manually by its actual value

- re-start ``Wzskcmbd``

``Wzskcmbd`` should now be serving the Vue.js app at http://127.0.0.1:13100. The CORS policy becomes obsolete in deployment configuration.

---

In case of problems, please do not hesitate to contact MPSI Technologles at [support@mpsitech.com](mailto:support@mpsitech.com).
