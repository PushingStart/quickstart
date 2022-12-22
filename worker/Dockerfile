FROM mcr.microsoft.com/dotnet/core/sdk:3.1@sha256:150d074697d1cda38a0c2185fe43895d84b5745841e9d15c5adba29604a6e4cb as builder

WORKDIR /Worker
COPY src/Worker/Worker.csproj .
RUN dotnet restore

COPY src/Worker/ .
RUN dotnet publish -c Release -o /out Worker.csproj

# app image
FROM mcr.microsoft.com/dotnet/core/runtime:3.1@sha256:bc18c2bf466481a9773822f3d29f681d866f7291895552609e75f2e7d76b9bcb

WORKDIR /app
ENTRYPOINT ["dotnet", "Worker.dll"]

COPY --from=builder /out .