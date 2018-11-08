# Import Path

You need to set import path to be normal

1. In your config find

        module.exports = {
            // ...
            resolve: {
                modules: ['node_modules']...
            }
        }

2. Make array look like this

        ['node_modules', paths.appNodeModules, 'src']

You should now be able to use imports like these

    import 'components/bla';