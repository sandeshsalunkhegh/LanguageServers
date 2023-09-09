FROM debian:10 as downloader

RUN apt-get update && apt-get install -y curl
RUN curl -L -o dotnet.tar.gz https://download.visualstudio.microsoft.com/download/pr/dd7d2255-c9c1-4c6f-b8ad-6e853d6bb574/c8e1b5f47bf17b317a84487491915178/dotnet-sdk-6.0.408-linux-x64.tar.gz
RUN mkdir -p /opt/dotnet && tar -zxf dotnet.tar.gz -C /opt/dotnet

RUN curl -L -o omnisharp.tar.gz https://github.com/OmniSharp/omnisharp-roslyn/releases/download/v1.39.8/omnisharp-linux-x64.tar.gz
RUN mkdir -p /opt/omnisharp && tar -zxf omnisharp.tar.gz -C /opt/omnisharp

FROM debian:10
# Install dependencies
RUN apt-get update \
  && apt-get install -y --no-install-recommends \
  curl \
  libicu-dev \
  libssl1.1 \
  libstdc++6 \
  ca-certificates \
  && rm -rf /var/lib/apt/lists/*

ENV DOTNET_RUNNING_IN_CONTAINER=true \
  NUGET_XMLDOC_MODE=skip \
  DOTNET_USE_POLLING_FILE_WATCHER=true \
  DOTNET_SYSTEM_NET_HTTP_USESOCKETSHTTPHANDLER=0

# Copy artifacts
COPY --from=downloader /opt/omnisharp /lsp-server/omnisharp
COPY --from=downloader /opt/dotnet /opt/dotnet

# COPY --from=downloader /opt/runtime /opt/runtime
RUN mkdir -p /workspace
COPY ./file.csproj /workspace
RUN ln -s /opt/dotnet/dotnet /usr/bin/dotnet

RUN dotnet nuget add source https://pkgs.dev.azure.com/dnceng/public/_packaging/dotnet-tools/nuget/v3/index.json -n dotnet-tools
RUN dotnet nuget add source https://pkgs.dev.azure.com/dnceng/public/_packaging/dotnet6/nuget/v3/index.json -n dotnet6
RUN dotnet nuget add source https://pkgs.dev.azure.com/dnceng/public/_packaging/dotnet6-transport/nuget/v3/index.json -n dotnet6-transport
RUN dotnet nuget add source https://www.myget.org/F/omnisharp/api/v3/index.json -n omnisharp

# Trigger first run experience by running arbitrary cmd to populate local package cache
RUN dotnet help
RUN cd /workspace && dotnet restore
RUN cp -r /opt/dotnet/host/fxr/6.0.16/libhostfxr.so /lsp-server/omnisharp/
RUN cp -r /opt/dotnet/shared/Microsoft.NETCore.App /lsp-server/omnisharp/

# These paths are hardcoded to avoid run script from omnisharp.
# Refer to the discussion on PR #30
# If something breaks, check the run script in omnisharp
ENV MONO_CFG_DIR=/lsp-server/omnisharp/etc
ENV MONO_ENV_OPTIONS="--assembly-loader=strict --config /lsp-server/omnisharp/etc/config"

ENV LANGUAGE='csharp'
