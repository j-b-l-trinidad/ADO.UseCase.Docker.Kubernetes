FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 8083
#EXPOSE 5000
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["ADO.UseCase.Docker.Kubernetes/ADO.UseCase.Docker.Kubernetes.csproj", "ADO.UseCase.Docker.Kubernetes/"]

RUN dotnet restore "ADO.UseCase.Docker.Kubernetes/ADO.UseCase.Docker.Kubernetes.csproj"
COPY . .
WORKDIR "/src/ADO.UseCase.Docker.Kubernetes"
RUN dotnet build "ADO.UseCase.Docker.Kubernetes.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ADO.UseCase.Docker.Kubernetes.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ADO.UseCase.Docker.Kubernetes.dll"]