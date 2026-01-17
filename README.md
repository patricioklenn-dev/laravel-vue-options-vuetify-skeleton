# Laravel Vue Skeleton

Laravel skeleton application with Vue.js, Inertia.js and Vuetify.

## Stack

- **Backend**: Laravel 12
- **Frontend**: Vue.js 3.5 with Inertia.js
- **UI Framework**: Vuetify 3
- **Build Tool**: Vite 6

## Features

- Authentication system (login, register, password reset, email verification)
- User profile management
- Modern UI with Vuetify components
- Spanish language support for validation messages

## Installation

1. Clone the repository
2. Install PHP dependencies: `composer install`
3. Install Node dependencies: `npm install`
4. Copy `.env.example` to `.env` and configure your database
5. Generate application key: `php artisan key:generate`
6. Run migrations: `php artisan migrate`
7. Build assets: `npm run dev` or `npm run build`

## Development

Run the development server:

```bash
npm run dev
```

Or use the composer script:

```bash
composer dev
```

## License

The Laravel framework is open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT).
