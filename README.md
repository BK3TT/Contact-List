# Contact-List

### Files will be added soon, you will be able to just clone the project

In this repository, you will be able to add contacts and also search through your current contacts list

Please keep reading on how to set this up. "Starting from Scratch"

This project has been done by using: 

- Laravel 5.7
- Bootstrap 4
- JQuery Datatables
- SQL (Database)

### Starting from Scratch

First you will need to make your Laravel project, run the following command:

```
composer create-project laravel/laravel contacts_list "5.7.*"
```

Once you have your Laravel project, you will need to go inside ```.env``` file and change the information for your database:

```
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=contact_list
DB_USERNAME=root
DB_PASSWORD=password
```

Then you will need to run the following command: 

```
php artisan make:migration contacts_table --create=Contacts
```
When this is generated it will be inside ```database->migrations```. You will want to open the outputted file and remove everything inside and copy the following:

```
<?php

use Illuminate\Support\Facades\Schema;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;

class ContactsTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('contacts', function (Blueprint $table) {
            $table->increments('id');
            $table->string('firstname')->index();
            $table->string('surname')->index();
            $table->string('email')->unique()->index();
            $table->string('phone')->unique()->index();
            $table->smallInteger('active')->default(1);
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::dropIfExists('contacts');
    }
}
```

Once you've saved, you will need to go into the ```config->database.php``` and update mysql engine line to the following: 

```
'engine' => 'InnoDB ROW_FORMAT=DYNAMIC',
```

Next run this following command and it will generate the contacts table in your local database:

```
php artisan migrate
```

After this we will need to make our Eloquent Model

```
php artisan make:model Contacts
```

Open the Contacts.php inside ```app->``` and remove everything inside and copy:

```
<?php

namespace App;

use Illuminate\Database\Eloquent\Model;

class Contacts extends Model
{
    protected $table = 'contacts';
    protected $fillable = [
        'firstname', 'surname', 'email', 'phone',
    ];
    public $timestamps = false;
}

?>
```

