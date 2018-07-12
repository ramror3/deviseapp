# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...

gem 'devise'

rails g devise:install

rails g devise User

rails g devise:views

config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }

config.action_mailer.delivery_method = :smtp

application.rb
 ActionMailer::Base.smtp_settings = {
      :address => "smtp.gmail.com",
      :domain => "mail.google.com",
      :port => "587",
      :user_name => "ramesh.win@gmail.com",
      :password => "password",
      :authentication => "login",
      :enable_starttls_auto => true
    }

rails g scaffold Post title:string content:text

rails g controller home index

create registration controller in controller

class RegistrationsController < Devise::RegistrationsController

  private

  def sign_up_params
    params.require(:user).permit(:name, :email, :password, :password_confirmation)
  end

  def account_update_params
    params.require(:user).permit(:name, :email, :password, :password_confirmation, :current_password)
  end
end

add this devise migration file

#username
t.string :name
      
routes

root 'home/index'

  resources :posts
  devise_for :users, controllers: { registrations: "registrations"}
  
add this in post controller
before_action :authenticate_user!


Home controller
def index
    if user_signed_in?
      redirect_to posts_path
    else
      redirect_to new_user_session_path
    end
  end

  Layouts

  <body>
    <% if user_signed_in? %>
      <p>Hello, <%= current_user.name %> - <%= link_to "sign_out", destroy_user_session_path, :method => 'delete' %></p>
      <br>
    <% end %>
    <%= yield %>

    rake db:migrate VERSION=0

    uncomment the confirmable in devise migrations


    rake db:migrate VERSION=0

    uncomment the lockable in devise migrations

    uncomment this lines in devise.rb

    config.lock_strategy = :failed_attempts

  # Defines which key will be used when locking and unlocking an account
  config.unlock_keys = [:email]

   config.unlock_strategy = :email

     config.maximum_attempts = 2
