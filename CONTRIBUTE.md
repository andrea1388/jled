## Prequisites

1. gcc, make, cpplint, lcov for the test and code quality checks
1. Arduino IDE/PlatformIO

## Contributing

The workflow is pretty standard:

1. Fork repository
1. Create your feature branch (`git checkout -b my-new-feature`)
1. Run the linter with `make lint`
1. [Run tests with `make test` and `make coverage`.](test/README.md)
1. Implement tests for your new feature - make sure test coverage does not decrease
1. Implement fixes
1. Commit your changes (`git commit -am 'Add some feature'`)
1. Push to a branch (`git push -u origin my-new-feature`)
1. Submit a pull request
