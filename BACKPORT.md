# Pinned edition search fix for Tubifarry 2.3.0.1

This branch contains the selected-edition fix from upstream PR #238 on the official v2.3.0.1 tag. The production change is six lines in the album request generator and the corresponding option hint. Other development-branch changes are excluded. Lidarr core is unchanged.

The regression suite invokes the real public indexer generator in eight cases: explicit longer and shorter editions, any-release mode, other count filters, absent selection and invalid selection. All eight pass with the pinned Lidarr submodule.

Build with .NET 8: `dotnet test Tubifarry.Tests/Tubifarry.Tests.csproj --configuration Release -p:CI=true -p:Branch=master -p:TreatWarningsAsErrors=false`.

This is a local backport, not a new upstream release. Runtime deployment requires a checked native backup/restore and an isolated plugin-load test. Return to an official package when this fix is released.
