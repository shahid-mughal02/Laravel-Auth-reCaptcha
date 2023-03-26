# Laravel Blog Canvas Template

## Laravel Installer Globally Setup
```
composer global require laravel/installer
```

## Install Laravel Project
```
laravel new project_name
```

## Install Breeze Authentication
```
composer require laravel/breeze --dev
php artisan breeze:install
```

## Install Packages 
```
npm install
```

## Build Application
```
npm run dev
```

## Migrate Tables
```
php artisan migrate
```

## Install Re-Captcha
```
composer require anhskohbo/no-captcha
```

In app/config/app.php add the following:
1- The ServiceProvider to the providers array:
```
Anhskohbo\NoCaptcha\NoCaptchaServiceProvider::class,
```

2- The class alias to the aliases array:
```
'NoCaptcha' => Anhskohbo\NoCaptcha\Facades\NoCaptcha::class,
```

3- Publish the config file
```
php artisan vendor:publish --provider="Anhskohbo\NoCaptcha\NoCaptchaServiceProvider"
```

Configuration
Add NOCAPTCHA_SECRET and NOCAPTCHA_SITEKEY in .env file:
```
NOCAPTCHA_SECRET=secret-key
NOCAPTCHA_SITEKEY=site-key
```
(Click me to get the Keys)[https://www.google.com/recaptcha/admin]

## Usage
Paste in Register/Login Page inside Form tag
```
{!! NoCaptcha::renderJs() !!}
{!! NoCaptcha::display() !!}
```

## Validation
Add 'g-recaptcha-response' => 'required|captcha' to rules array in RegisterUserController:
```
$validate = Validator::make(Input::all(), [
	'g-recaptcha-response' => 'required|captcha'
]);
```

## Then check for captcha errors in the Form :
```
@if ($errors->has('g-recaptcha-response'))
    <span class="help-block">
        <strong>{{ $errors->first('g-recaptcha-response') }}</strong>
    </span>
@endif
```

## Run Project Artisan
```
php artisan serve
```