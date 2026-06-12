# Agents

The `fsuipc-test-client/` directory is a .NET 10 console application with Windows dependencies (FSUIPCClientDLL).

Before declaring work complete, always run formatter, tests, build.

```bash
# Format
dotnet format fsuipc-test-client 
dotnet format fsuipc-test-client.Tests

# Build
dotnet build fsuipc-test-client

# Test
dotnet test fsuipc-test-client.Tests

# Run (TUI mode)
dotnet run --project fsuipc-test-client -- slc-offsets.csv

# Run (batch mode)
dotnet run --project fsuipc-test-client -- slc-offsets.csv --batch > output.json
```