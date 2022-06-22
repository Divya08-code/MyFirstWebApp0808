#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["MyFirstWebApp0808/MyFirstWebApp0808.csproj", "MyFirstWebApp0808/"]
RUN dotnet restore "MyFirstWebApp0808/MyFirstWebApp0808.csproj"
COPY . .
WORKDIR "/src/MyFirstWebApp0808"
RUN dotnet build "MyFirstWebApp0808.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MyFirstWebApp0808.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MyFirstWebApp0808.dll"]