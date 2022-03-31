#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.




FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["DLTest/DLTest.csproj", "DLTest/"]
RUN dotnet restore "DLTest/DLTest.csproj"
COPY . .
WORKDIR "/src/DLTest"
RUN dotnet build "DLTest.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DLTest.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DLTest.dll"]