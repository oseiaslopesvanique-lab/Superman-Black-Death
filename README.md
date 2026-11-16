name: Build Superman Black Death

on:
  workflow_dispatch:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: '8'

      - uses: gradle/actions/setup-gradle@v4
        with:
          gradle-version: '4.10.3'

      - name: Extract project
        run: |
          unzip -o Superman_Black_Death_Forge_1.12.2_2859_visual_revisado.zip -d source

      - name: Build mod
        working-directory: source
        run: gradle build

      - name: Upload JAR
        uses: actions/upload-artifact@v4
        with:
          name: SupermanBlackDeath
          path: source/build/libs/*.jar
