// Make a set of all api modules we wish to use
setOf(
    "fabric-api-base",
    "fabric-command-api-v1",
    "fabric-lifecycle-events-v1",
    "fabric-networking-api-v1"
).forEach {
    // Add each module as a dependency
    modImplementation(fabricApi.module(it, FABRIC_API_VERSION))
}

Written by the community, these guides cover a wide range of topics, from setting up your development environment to more advanced areas like rendering and networking.

Check out the sidebar for a list of all available guides. If you're searching for something specific, the search bar at the top of the page is your best friend.

Remember: a fully-working mod with all the code for this documentation is available in the [`/reference` folder on GitHub](https://github.com/FabricMC/fabric-docs/tree/main/reference/latest).

If you want to contribute to the Fabric Documentation, you can find the source code on [GitHub](https://github.com/FabricMC/fabric-docs), and the relevant [contribution guidelines](../contributing).
