# laravel-graphql-upload
GraphQL Upload middleware for Laravel and Lumen 

This package is ported from https://github.com/Ecodev/graphql-upload

## Install
```bash
composer require axe/laravel-graphql-upload
```

## Usage
> example use with _Folklore\GraphQL_

### in the config/graphql file, use the middleware
```php
    'middleware' => [
        Axe\LaravelGraphQLUpload\GraphqlUploadMiddleware::class
    ]
```

### in your mutation:
```php
<?php

namespace App\GraphQL\Mutation;

use Axe\LaravelGraphQLUpload\UploadType;
use Folklore\GraphQL\Support\Mutation;
use GraphQL;


class UploadFileMutation extends Mutation
{


    public function type()
    {
        return GraphQL::type('YourReturnType');
    }

    public function args()
    {
        return [
            "file" => ['name' => 'file', 'type' => UploadType::type()],
        ];
    }

    public function rules()
    {
        return [
            'file' => 'required|file|mimes:csv,txt',
        ];
    }

    public function resolve($root, $args)
    {
        $file = $args['file'];

        // call some function
        $path = $file->getRealPath();

        // ... your logic here
    }
}
```