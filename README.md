## Laravel-Vue-Inertia-Starter-Setup

<br>

## Setup

1. Install Composer Dependencies:
    ```
    composer install
    ```
    <br>
2. Install NPM Dependencies:
    ```
    npm install
    ```
    <br>
3. Create a new .env file (copy of env.example):
    ```
    cp .env.example .env
    ```
    <br>
4. Generate an app encryption key:
    ```
    php artisan key:generate
    ```
    <br>
5. In the .env file, add your database name, username & password. 
    <br>
6. Run migrations:
    ```
    php artisan migrate
    ```
    <br>
7. Run app:
    ```
    php artisan serve
    ```
    <br>
8. To compile assets (Mix) run :
    ```
    npm run dev
    ```
    <br>
    <br>
## Docs
- [Laravel](https://laravel.com/docs)
- [Laravel Sanctum](https://laravel.com/docs/8.x/sanctum)
- [Vue.js](https://vuejs.org/)
- [Tailwindcss](https://tailwindcss.com/docs/installation)
    <br>
    <br>
## Starter creation guide:
1. SERVER-SIDE SETUP
    1. Install inertia : 
        ```
        composer require inertiajs/inertia-laravel 
        ```
    2. Setup root app.blade.php file by adding scripts, css and @inertia directive
    3. Publish Inertia middleware : 
        ```
        php artisan inertia:middleware
        ```
    4. Add middleware in app\kernel.php web middleware section :
        \App\Http\Middleware\HandleInertiaRequests::class,
    <br>
2. CLIENT-SIDE SETUP
    1. Install inertia, inertia vue driver, vue and vue-template-compiler : 
        ```
        npm install @inertiajs/inertia @inertiajs/inertia-vue vue
        npm install vue-template-compiler --save-dev
        ```
    2. In app.js (or other main js file) initialize inertia and vue:
        ```
        import { App, plugin } from '@inertiajs/inertia-vue'
            import Vue from 'vue'

            Vue.use(plugin)
                const el = document.getElementById('app')
                new Vue({
            render: h => h(App, {
                    props: {
                initialPage: JSON.parse(el.dataset.page),
                    resolveComponent: name => require(`./Pages/${name}`).default,
                },
        }),
        }).$mount(el)
        ```
    3. In resources\js create Pages folder
    4. Install node dependencies and compile assets
        ```
        npm install & npm run dev
        ```   
    5. (Optional) To use code splitting with Inertia you'll need to enable dynamic imports: 
        ```
        npm install @babel/plugin-syntax-dynamic-import;
        ```
        - Next create .babelrc in the root with and add:
        ```
        {
        "plugins": ["@babel/plugin-syntax-dynamic-import"]
        }
        ```
        - Finally, update the resolveComponent callback in your app initialization to use import instead of require:
        ```php
            resolveComponent: name => import(`./Pages/${name}`).then(module => module.default),
        ```