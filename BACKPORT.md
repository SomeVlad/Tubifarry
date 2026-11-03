# Pinned edition search fix for Tubifarry 2.3.0.1

This branch contains the selected-edition fix from upstream PR #238 on the official v2.3.0.1 tag. The production change is six lines in the album request generator and the corresponding option hint. Other development-branch changes are excluded. Lidarr core is unchanged.

The regression suite invokes the real public indexer generator in eight cases: explicit longer and shorter editions, any-release mode, other count filters, absent selection and invalid selection. All eight pass with the pinned Lidarr submodule.

Build with .NET 8: `dotnet test Tubifarry.Tests/Tubifarry.Tests.csproj --configuration Release -p:CI=true -p:Branch=master -p:TreatWarningsAsErrors=false`.

This is a local backport, not a new upstream release. Runtime deployment requires a checked native backup/restore and an isolated plugin-load test. Return to an official package when this fix is released.

For a runtime package, first build `Submodules/Lidarr/src/Lidarr.Http/Lidarr.Http.csproj` with `-p:AssemblyVersion=3.1.6.5102` so all three reference assemblies match the deployed core. Then build the plugin and tests with `-p:Version=2.3.0.1 -p:AssemblyVersion=2.3.0.1 -p:MinimumLidarrVersion=3.1.6.5102 -p:BuildProjectReferences=false`. Verify the plugin's three Lidarr references before packaging. The vendored core uses a placeholder `10.0.0.*` identity outside its official CI; the reference-build identity must match the real deployed core. No core code is modified or deployed.
