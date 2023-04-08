FROM mcr.microsoft.com/dotnet/runtime:7.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["IcebreakerTalkBot/IcebreakerTalkBot.csproj", "IcebreakerTalkBot/"]
RUN dotnet restore "IcebreakerTalkBot/IcebreakerTalkBot.csproj"
COPY . .
WORKDIR "/src/IcebreakerTalkBot"
RUN dotnet build "IcebreakerTalkBot.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "IcebreakerTalkBot.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "IcebreakerTalkBot.dll"]
