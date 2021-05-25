# Updating Data

As you are working, it is very likely that you will be
making changes at `admin.sitechef.co.uk` at the same time
as you are changing your code locally.

If you want to update your local code with data from the server:

1. Create a `JSON snapshot` on at `admin.sitechef.co.uk` by navigating to 
    [Theme Manager](https://admin.sitechef.co.uk/wizard/theme)
    and clicking `Generate JSON Snapshot`
2. Once this is complete run `sitechef update` at the root of your project
3. If you were running `sitechef serve` at the time, this will need to be 
    run again to be up-to-date with the latest data