# Safe Redirect

A little gem to keep our Rails app safe from open redirection vulnerabilities.

## Installation

Add this line to Gemfile.

```
gem 'safe_redirect'
```

##  Usage

Create a `config/initializer/safe_redirect.rb` file.

```rb
SafeRedirect.configure do |config|
  config.default_path = 'https://www.yahoo.com' # default value: '/'
  config.domain_whitelists = ['www.google.com'] # default value: []
end
```

Add this line to the controllers you wish to secure from open redirection.

```rb
include SafeRedirect
```

The `redirect_to` method provided by Rails will be overridden by `safe_redirect`'s `redirect_to` method.

```rb
redirect_to 'https://www.google.com' # => redirects to https://www.google.com
redirect_to 'https://www.golgege.com' # => redirects to '/'
redirect_to 'https://www.golgege.com', safe: true # => redirects to 'https://www.golgege.com'
redirect_to 'https://www.golgege.com/hahaha' # => redirects to '/hahaha'
redirect_to 1234 # => redirects to https://www.yahoo.com as default path
```

## Contributing

- Fork the repository
- Create a branch for a new feature or bug fix, build it
- Create a pull request

## License

MIT License

## Author

- [Edwin Tunggawan](https://github.com/sdsdkkk)
