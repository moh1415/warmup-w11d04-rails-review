# Rails Review

For each of the following topics, please answer each of the questions. You can use links and images to support your answer. Once done please make a pull request.

## Has many Through

- [Rails Active Record Intro](https://github.com/sei-entropy/lesson-w11d02-rails-active-record#active-record-associations)
-[Hospital App](https://github.com/sei-entropy/hw-w11d02-rails-hospital)

### Questions

1. What is the role of a join table in a many-to-many relationship?
`create table hold the many to many relationship`
2. What two columns must be present in a join table?
`id column from both table`

3. Given the example below, edit the code to define a has many :through relationship.

    ```ruby
    class Customer < ActiveRecord::Base
    has_many :product
    end

    class Product < ActiveRecord::Base
    has_many :customer
    end

    class Purchase < ActiveRecord::Base
    has_and_belongs_to_many :customer 
    end
    ```


4. Based on #3, give an example of associating two instances via the join model.
``` ruby
create_join_table :products, :categories do |t|
  t.index :product_id
  t.index :category_id
end
```


## Devise

- [Devise Lesson](https://github.com/sei-entropy/lesson-w11d03-rails-devise)

### Questions

1. What does the `current_user` method that the Devise gem provides?
`give you current username or email that been has login.`

2. What does the `authenticate_user!` method that the Devise gem provides?
`limit access to some router and the controller.`

3. Write a signout link using the `link_to` rails helper and a devise path.
`<% if user_signed_in? %>`
`<li><%= link_to  "Sign Out", destroy_user_session_path, method: :delete %></li>`
  `<% end %>`

4. How do I generate a devise model in the terminal?
`rails generate devise MODEL`

5. What are the trade offs for using a gem for authentication over a handrolled solution? (no real right answer)
`more security and you modifite`


## Validations

- [Validations Lesson](https://github.com/sei-entropy/lesson-w11d03-rails-model-validations)

### Questions

1. Which component, of Rails MVC, is responsible for the business logic?
`MODEL`

2. Assume the user's age is an optional field.  Write the validation to verify that a User's age is between 13 and 125 (inclusive).
 `validates :age, inclusion: { in: %w(small medium large)`
3. What would `user.errors.messages` return (for the above User), if you assigned `user.age = 12`?
`wrong value of age`

4. Assume you visit "/customers/new" and enter some invalid information.  Given this controller code, what url would your browser be on after pressing "Create Customer"?
 `render the same page /customers/new`
``` ruby
class CustomersController < ApplicationController
  def new
    @customer = Customer.new
  end

  def create
    @customer = Customer.new(customer_params)
    if @customer.save
      redirect_to customer_path(@customer)
    else
      render :new
    end
  end
  ...
  private
  def customer_params
    params.require(:customer).permit(:first_name, :last_name, :age)
  end
end
```


5. Give one reason why we might have the similar validations in the browser, model, and database layer of our application.
`give you more security rather in using browser js cause we can disable it`

