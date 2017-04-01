# Minitest::MockRaiseError

A simple Minitest mock extension to raise error.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'minitest-mock_raise_error'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install minitest-mock_raise_error

## Usage

Require `minitest/mock_raise_error` in your test_helper.rb before `require 'minitest/autorun''`.

```ruby
require 'minitest/mock_raise_error'
require 'minitest/autorun'
```

Next, call `Minitest::Mock#expect` with a exception or a subclass of Exception as ret_val.
Then, the mock raises error with a specified exception or a instance of subclass of Exception. 

```ruby
class MyTestError < StandardError; end

# With a exception
mock = Minitest::Mock.new
error = MyTestError.new('error message')
mock.expect(:my_test, error)
begin
  mock.my_test
  fail
rescue MyTestError => e
  e # => #<MyTestError: error message>
end
mock.verify # => true

# With a subclass of Exception
mock = Minitest::Mock.new
mock.expect(:my_test2, MyTestError)
begin
  mock.my_test2
  fail
rescue MyTestError => e
  e # => #<MyTestError: MyTestError>
end
mock.verify # => true
```

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/ryu39/minitest-mock_raise_error. 

This project is intended to be a safe, welcoming space for collaboration, 
and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.

If you want to send pull requests, please follow these steps.

1. Fork this repository.
2. Clone the forked repository.
3. Execute `bin/setup`.
4. Execute `bundle exec rake` and check there are no failed test or offences.
5. Create and check out your feature branch.
6. Commit your changes.
7. Execute `bundle exec rake` and confirm again.
8. Push your branch.
9. Create pull requests to master branch!!

## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).

