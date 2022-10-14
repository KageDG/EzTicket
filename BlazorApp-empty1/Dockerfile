FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["BlazorApp-empty1/BlazorApp-empty1.csproj", "BlazorApp-empty1/"]
RUN dotnet restore "BlazorApp-empty1/BlazorApp-empty1.csproj"
COPY . .
WORKDIR "/src/BlazorApp-empty1"
RUN dotnet build "BlazorApp-empty1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BlazorApp-empty1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BlazorApp-empty1.dll"]
