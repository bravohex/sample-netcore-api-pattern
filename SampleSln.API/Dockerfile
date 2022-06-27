#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["SampleSln.API/SampleSln.API.csproj", "SampleSln.API/"]
RUN dotnet restore "SampleSln.API/SampleSln.API.csproj"
COPY . .
WORKDIR "/src/SampleSln.API"
RUN dotnet build "SampleSln.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SampleSln.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SampleSln.API.dll"]