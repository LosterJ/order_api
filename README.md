b1: Create laravel project
    
    composer create-project laravel/laravel order_api
    cd order_api

b2: Setup db

b3: make model Order

    php artisan make:model Order -a
    (-a argument will create migration,seeder,factory,controller)

- update "up" function in migration (change column in db)
- update "definition" function in factory (fake data)
- update "run" function in seeder
    use App\Models\Order;
    Order::factory()->time(50)->create();
- update "run" function in DatabaseSeeder.php to run OrderSeeder
    $this->call(
        [
            OrderSeeder::class
        ]
    );
- run migrations and seed the db
    php artisan migrate --seed

b4: create repository

- create folder "Interfaces" then create new file "OrderRepositoryInterface.php"
- create folder "Repositories" then create new file "OrderRepository.php"

b5: create controllers

- update OrderController.php

b6: add route in routes/api.php

- import OrderController

b7: bind interface and implementation

- bind by Service Provider
    php artisan make:provider RepositoryServiceProvider
- update "register" function in Provider
    use App\Interfaces\OrderRepositoryInterface;
    use App\Repositories\OrderRepository;
    $this->app->bind(OrderRepositoryInterface::class, OrderRepository::class);
- add new serviceprovider to "providers" array in config/app.php
