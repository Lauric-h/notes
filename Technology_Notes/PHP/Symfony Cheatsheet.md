#learnings #language #php #framework #php 

# Symfony Cheatsheet
## Symfony CLI commands
**Add or update an entity**  
`symfony console make:entity`    

**Make migration**  
`symfony console make:migration`   

**Apply migration to DB**  
`symfony console doctrine:migrations:migrate`
`symfony console d:m:m`

**Make unit test**  
`symfony console make:test TestCase NameOfTest` 

**Run tests**  
`php bin/phpunit --testdox`

**Add Controller**  
`symfony console make:controller NameOfController`    

**Make auth**  
`symfony console make:auth`  

**Load fixtures**  
`symfony console doctrine:fixtures:load`  

## Tests
### Unit Tests
- Create unit test with the Symfony CLI command `symfony console make:test TestCase NameOfTest` 
- In `/tests`, add your unit tests
- Run them with `php bin/phpunit --testdox`  

**Example simple unit test**  

```php
public function testIsTrue() {  
 $user = new User();  
  
 $user->setEmail('true@test.com')  
 ->setFirstname('Lauric')  
 ->setLastname('Lastname')  
 ->setAbout('Description');  
  
 $this->assertTrue($user->getEmail() === 'true@test.com');  
 $this->assertTrue($user->getFirstname() === 'Lauric');  
 $this->assertTrue($user->getLastname() === 'Lastname');  
 $this->assertTrue($user->getAbout() === 'Description');  
}  
  
public function testIsFalse() {  
 $user = new User();  
  
 $user->setEmail('true@test.com')  
 ->setFirstname('Lauric')  
 ->setLastname('Lastname')  
 ->setAbout('Description');  
  
 $this->assertFalse($user->getEmail() === 'false@test.com');  
 $this->assertFalse($user->getFirstname() === 'false');  
 $this->assertFalse($user->getLastname() === 'false');  
 $this->assertFalse($user->getAbout() === 'false');  
}  
  
public function testIsEmpty() {  
 $user = new User();  
  
 $this->assertEmpty($user->getEmail());  
 $this->assertEmpty($user->getFirstname());  
 $this->assertEmpty($user->getLastname());  
 $this->assertEmpty($user->getAbout());  
}

```