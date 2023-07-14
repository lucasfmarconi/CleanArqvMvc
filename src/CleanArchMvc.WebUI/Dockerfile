#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["src/Directory.Build.props", "src/"]
COPY ["Directory.Build.props", "."]
COPY ["src/CleanArchMvc.WebUI/CleanArchMvc.WebUI.csproj", "src/CleanArchMvc.WebUI/"]
COPY ["src/CleanArchMvc.Infra.IoC/CleanArchMvc.Infra.IoC.csproj", "src/CleanArchMvc.Infra.IoC/"]
COPY ["src/CleanArchMvc.Domain/CleanArchMvc.Domain.csproj", "src/CleanArchMvc.Domain/"]
COPY ["src/CleanArchMvc.Application/CleanArchMvc.Application.csproj", "src/CleanArchMvc.Application/"]
COPY ["src/CleanArchMvc.Infra.Data/CleanArchMvc.Infra.Data.csproj", "src/CleanArchMvc.Infra.Data/"]
RUN dotnet restore "src/CleanArchMvc.WebUI/CleanArchMvc.WebUI.csproj"
COPY . .
WORKDIR "/src/src/CleanArchMvc.WebUI"
RUN dotnet build "CleanArchMvc.WebUI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CleanArchMvc.WebUI.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CleanArchMvc.WebUI.dll"]