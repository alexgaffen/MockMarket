# Build stage: compiler, CMake and the nlohmann/json headers.
FROM ubuntu:22.04 AS build
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y --no-install-recommends     build-essential     cmake     nlohmann-json3-dev     && rm -rf /var/lib/apt/lists/*
WORKDIR /app
COPY CMakeLists.txt .
COPY src ./src
RUN cmake -S . -B build -DCMAKE_BUILD_TYPE=Release && cmake --build build

# Runtime stage: just the binary.
FROM ubuntu:22.04
COPY --from=build /app/build/cpp_service /usr/local/bin/cpp_service
EXPOSE 8080
CMD ["cpp_service"]
