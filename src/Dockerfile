FROM minecase.dotnet AS builder

WORKDIR /build

ADD stylecop.json Analyzers.ruleset /build/
ADD data/                           /build/data/
ADD MineCase.Algorithm/             /build/MineCase.Algorithm/
ADD MineCase.CodeGeneration/        /build/MineCase.CodeGeneration/
ADD MineCase.Core/                  /build/MineCase.Core/
ADD MineCase.Protocol/              /build/MineCase.Protocol/
ADD MineCase.Nbt/                   /build/MineCase.Nbt/
ADD MineCase.Server/                /build/MineCase.Server/
ADD MineCase.Serialization/         /build/MineCase.Serialization/
ADD MineCase.Server.Grains/         /build/MineCase.Server.Grains/
ADD MineCase.Engine/                /build/MineCase.Engine/
ADD MineCase.Server.Interfaces      /build/MineCase.Server.Interfaces/

RUN dotnet publish MineCase.Server/MineCase.Server.csproj

FROM minecase.dotnet

ARG RELEASE_PROFILE=Release
ARG TARGET_FRAMEWORK=net5.0

WORKDIR /app
EXPOSE 30000

COPY --from=builder /build/MineCase.Server/bin/${RELEASE_PROFILE}/${TARGET_FRAMEWORK}/publish/ .

ENTRYPOINT ["dotnet", "MineCase.Server.dll"]
