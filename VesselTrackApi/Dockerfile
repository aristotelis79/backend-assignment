FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["VesselTrackApi/VesselTrackApi.csproj", "VesselTrackApi/"]
RUN dotnet restore "VesselTrackApi/VesselTrackApi.csproj"
COPY . .
WORKDIR "/src/VesselTrackApi"
RUN dotnet build "VesselTrackApi.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "VesselTrackApi.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "VesselTrackApi.dll"]