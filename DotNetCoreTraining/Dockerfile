#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-nanoserver-1803 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-nanoserver-1803 AS build
WORKDIR /src
COPY ["DotNetCoreTraining/DotNetCoreTraining.csproj", "DotNetCoreTraining/"]
RUN dotnet restore "DotNetCoreTraining/DotNetCoreTraining.csproj"
COPY . .
WORKDIR "/src/DotNetCoreTraining"
RUN dotnet build "DotNetCoreTraining.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DotNetCoreTraining.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DotNetCoreTraining.dll"]