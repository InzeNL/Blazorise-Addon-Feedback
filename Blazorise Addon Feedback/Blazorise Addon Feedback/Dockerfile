#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Blazorise Addon Feedback/Blazorise Addon Feedback.csproj", "Blazorise Addon Feedback/"]
RUN dotnet restore "Blazorise Addon Feedback/Blazorise Addon Feedback.csproj"
COPY . .
WORKDIR "/src/Blazorise Addon Feedback"
RUN dotnet build "Blazorise Addon Feedback.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Blazorise Addon Feedback.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Blazorise Addon Feedback.dll"]