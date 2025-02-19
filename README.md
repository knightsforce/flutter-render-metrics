# Render Metrics

<img src="https://raw.githubusercontent.com/surfstudio/flutter-open-source/main/assets/logo_black.png#gh-light-mode-only" width="200">
<img src="https://raw.githubusercontent.com/surfstudio/flutter-open-source/main/assets/logo_white.png#gh-dark-mode-only" width="200">

Made by [Surf 🏄‍♂️🏄‍♂️🏄‍♂️](https://surf.dev/)

[![Build Status](https://shields.io/github/actions/workflow/status/surfstudio/flutter-render-metrics/main.yml?logo=github&logoColor=white)](https://github.com/surfstudio/flutter-render-metrics)
[![Coverage Status](https://img.shields.io/codecov/c/github/surfstudio/flutter-render-metrics?=render_metrics&logo=codecov&logoColor=white)](https://app.codecov.io/gh/surfstudio/flutter-render-metrics)
[![Pub Version](https://img.shields.io/pub/v/render_metrics?logo=dart&logoColor=white)](https://pub.dev/packages/render_metrics)
[![Pub Likes](https://badgen.net/pub/likes/render_metrics)](https://pub.dev/packages/render_metrics)
[![Pub popularity](https://badgen.net/pub/popularity/render_metrics)](https://pub.dev/packages/render_metrics/score)
![Flutter Platform](https://badgen.net/pub/flutter-platform/render_metrics)

## Overview

This package helps retrieve the current positioning coordinates of any widget in a widgets tree in your Flutter application.

## Currently supported features

- Retrieve the full set of positioning coordinates of the desired widget at any time;
- Calculate the difference in positioning between two widgets and use it the way you need.

## Example

### Getting widget's coordinates

Instantiate `RenderParametersManager` object. You can set a special type for the widget's unique identifier or leave it `dynamic`.

```dart
final renderManager = RenderParametersManager<dynamic>();
```

Wrap the desired widget in a `RenderMetricsObject`. The `id` parameter is the widget’s unique identifier.

```dart
RenderMetricsObject(
    id: "uniqueWidgetId",
    manager: renderManager,
    child: Container(
        ...
    ),
),
```

Get a bundle with the positioning coordinates of the wrapped widget.

```dart
RenderData data = renderManager.getRenderData("uniqueWidgetId");
```

### Calculating the difference in positioning between two widgets

Wrap the widgets you want to compare in `RenderMetricsObject`s. Specify two different `id`s for each of them. Please note, that the `manager` parameter of both widgets should contain the link to the same `RenderParametersManager` instance.

```dart
RenderMetricsObject(
    id: "rowWidgetId",
    manager: renderManager,
    child: Row(
        ...
    ),
),
RenderMetricsObject(
    id: "columnWidgetId",
    manager: renderManager,
    child: Column(
        ...
    ),
),
```

Specify two unique widget identifiers when using the `getDiffById()` function and extract a bundle with the relative difference in positioning coordinates between the widgets.

```dart
ComparisonDiff diff =
    renderManager.getDiffById("rowWidgetId", "columnWidgetId");
```

## What metrics can I get?

### RenderData

`RenderData` instance contains a complete set of properties that characterize any widget in a two-dimensional space.

All metrics positioning coordinates are global, meaning they are relative to the entire screen coordinate space.

![RenderData](https://i.ibb.co/CzCWkSB/render-data-1.png)

`RenderData` also provides you an ability to get all widget keypoint XY-coordinates by calling one of special getters.

![RenderData](https://i.ibb.co/DQzt33H/render-data-2.png)

### ComparisonDiff

You can get the comparison relative results for each widget keypoint from the `ComparisonDiff` instance.

An additional set of special getters can help you calculate the difference between two adjacent sides of two different widgets (e.g. right to left, top to bottom, etc.).

![RenderData](https://i.ibb.co/SNMPztt/render-diff.png)

## Installation

Add `render_metrics` to your `pubspec.yaml` file:

```yaml
dependencies:
  render_metrics: $currentVersion$
```

<p>At this moment, the current version of <code>render_metrics</code> is <a href="https://pub.dev/packages/render_metrics"><img style="vertical-align:middle;" src="https://img.shields.io/pub/v/render_metrics.svg" alt="render_metrics version"></a>.</p>

## Changelog

All notable changes to this project will be documented in [this file](./CHANGELOG.md).

## Issues

To report your issues, submit them directly in the [Issues](https://github.com/surfstudio/flutter-render-metrics/issues) section.

## Contribute

If you would like to contribute to the package (e.g. by improving the documentation, fixing a bug or adding a cool new feature), please read our [contribution guide](./CONTRIBUTING.md) first and send us your pull request.

Your PRs are always welcome.

## How to reach us

Please feel free to ask any questions about this package. Join our community chat on Telegram. We speak English and Russian.

[![Telegram](https://img.shields.io/badge/chat-on%20Telegram-blue.svg)](https://t.me/SurfGear)

## License

[Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0)
