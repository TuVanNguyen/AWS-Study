# AWS CLI

## Pagination
* control number of items returned in output from running a command
* default: size = 1000

### Pagination Errors
* Time Out Errors
    * pagination size is too high, taking too long to return all the items
    * fix: change page size with `--page-size` option
        