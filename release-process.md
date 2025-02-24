# Cutting a new release of the Spin Kinesis trigger plugin

To cut a new release of the kinesis trigger plugin, you will need to do the following:

1. Confirm that [CI is green](https://ogghead/spin-trigger-kinesis/actions) for the commit selected to be tagged and released.

1. Change the version number in [Cargo.toml](./Cargo.toml) and [spin-pluginify.toml](./spin-pluginify.toml) and run `cargo build --release`.

1. Create a pull request with these changes and merge once approved.

1. Checkout the commit with the version bump from above.

1. Create and push a new tag with a `v` and then the version number.

    As an example, via the `git` CLI:

    ```
    # Create a GPG-signed and annotated tag
    git tag -s -m "Spin Kinesis Trigger v0.2.0" v0.2.0

    # Push the tag to the remote corresponding to ogghead/spin-trigger-kinesis (here 'origin')
    git push origin v0.2.0
    ```

1. Pushing the tag upstream will trigger the [release action](https://github.com/ogghead/spin-trigger-kinesis/actions/workflows/release.yml).
    - The release build will create the packaged versions of the plugin, the updated plugin manifest and a checksums file
    - These assets are uploaded to a new GitHub release for the pushed tag
    - Release notes are auto-generated but edit as needed especially around breaking changes or other notable items
  
1. Create a PR in the [ogghead/spin-plugins](https://github.com/ogghead/spin-plugins) repository with the [updated manifest](https://github.com/ogghead/spin-plugins/tree/main/manifests/kinesis-trigger).
