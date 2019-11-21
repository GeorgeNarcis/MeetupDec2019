FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["MeetupWebAPI1/MeetupWebAPI1.csproj", "MeetupWebAPI1/"]
RUN dotnet restore "MeetupWebAPI1/MeetupWebAPI1.csproj"
COPY . .
WORKDIR "/src/MeetupWebAPI1"
RUN dotnet build "MeetupWebAPI1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MeetupWebAPI1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MeetupWebAPI1.dll"]