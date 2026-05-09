	FROM mcr.microsoft.com/dotnet/asnet:"8.0 AS base
	WORKDIR /app
	EXPOSE ASPNETCORE_URLS=http://+:8080


	FROM mcr.microsoft.com/dotnet/asnet:"8.0 AS Build
	WORKDIR /src
	COPY . .
	RUN  dotnet restore
	RUN dotnet publish -c Release -o /app/out

	FROM base AS final
	WORKDIR /app
	COPY --from=build /app/out
	ENTRYPOINT ["dotnet","BotonLibraryNowAPI.dll"]s

	
