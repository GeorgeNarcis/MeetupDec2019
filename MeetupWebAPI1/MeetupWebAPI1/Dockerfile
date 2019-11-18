#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-nanoserver-1809 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-nanoserver-1809 AS build
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