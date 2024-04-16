# Adding Dependencies with TOML

When using the version catalog approach with the `libs.versions.toml` file in your Android project, you can centralize dependency versions and easily reference them in your Gradle files. Here's how you can update the TOML file to include Hilt and Retrofit dependencies:

## Updating `libs.versions.toml`

```toml
[versions]
hilt = "2.44"
retrofit = "2.9.0"

[libraries]
# Hilt
hilt-android = { group = "com.google.dagger", name = "hilt-android", version.ref = "hilt" }
hilt-compiler = { group = "com.google.dagger", name = "hilt-compiler", version.ref = "hilt" }

# Retrofit
retrofit-core = { group = "com.squareup.retrofit2", name = "retrofit", version.ref = "retrofit" }
retrofit-converter-gson = { group = "com.squareup.retrofit2", name = "converter-gson", version.ref = "retrofit" }

[plugins]
hilt-plugin = { id = "com.google.dagger.hilt.android", version.ref = "hilt" }
```

In the `[versions]` section, define the versions for Hilt and Retrofit.

In the `[libraries]` section, define the library dependencies:
- `hilt-android` and `hilt-compiler` for Hilt.
- `retrofit-core` for the Retrofit core library.
- `retrofit-converter-gson` for the Gson converter factory for Retrofit.

In the `[plugins]` section, define the Hilt Gradle plugin.

## Updating `build.gradle`

Update your module-level `build.gradle` file to use the dependencies defined in the TOML file:

```groovy
plugins {
    id 'com.android.application' // or 'com.android.library'
    id 'kotlin-android'
    id 'kotlin-kapt'
    id libs.plugins.hilt.plugin.get().pluginId
}

dependencies {
    // ...

    // Hilt
    implementation libs.hilt.android
    kapt libs.hilt.compiler

    // Retrofit
    implementation libs.retrofit.core
    implementation libs.retrofit.converter.gson

    // ...
}
```

In the `plugins` block, apply the Hilt Gradle plugin using the version catalog reference.

In the `dependencies` block, use the version catalog references to include the Hilt and Retrofit dependencies.

Remember to sync your Gradle files after making these changes to ensure that the dependencies are properly resolved.

By updating the `libs.versions.toml` file and referencing the dependencies in your Gradle files, you can easily manage and update the versions of Hilt and Retrofit across your project.
