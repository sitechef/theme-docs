#The ".sitechefrc" file

When placed at the root of the theme directory, the `.sitechefrc` file
provides advanced configuration options for the SiteChef CLI.

It is a JSON file with the following fields:

    {
      /**
       * ignore: an array of folders that SiteChef
       *         should not publish back to the server
       *         Include any private files or files
       *         that are generated on installation
       */
      "ignore": [
        "node_modules",
        "anyFilesStartingWith*",
        "anyPathStartingWith**"
      ],
      /**
       * compileCommand: an array of the sections of
       *          the relative path that will be executed
       *          on "sitechef serve"
       *          In the example below, it will execute
       *          "./node_modules/.bin/gulp"
       *          If you wish to use an alternative asset
       *          generation tool like grunt, the array would
       *          be: ["grunt watch"]
       */
      "compileCommand":[
        "node_modules",
        ".bin",
        "gulp"
      ]
    }

*N.B the `.sitechefrc` file must be valid JSON. The comments above would
invalidate the JSON and have only been included here to explan to clarify the
explanation.*
