#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-nanoserver-1809 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-nanoserver-1809 AS build
WORKDIR /src
COPY ["MeetupWebAPI2/MeetupWebAPI2.csproj", "MeetupWebAPI2/"]
RUN dotnet restore "MeetupWebAPI2/MeetupWebAPI2.csproj"
COPY . .
WORKDIR "/src/MeetupWebAPI2"
RUN dotnet build "MeetupWebAPI2.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MeetupWebAPI2.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MeetupWebAPI2.dll"]