# Welcome to your Expo app 👋

This is an [Expo](https://expo.dev) project created with [`create-expo-app`](https://www.npmjs.com/package/create-expo-app).

## Get started

1. Install dependencies

   ```bash
   npm install
   ```

2. Start the app

   ```bash
   npx expo start
   ```

In the output, you'll find options to open the app in a

- [development build](https://docs.expo.dev/develop/development-builds/introduction/)
- [Android emulator](https://docs.expo.dev/workflow/android-studio-emulator/)
- [iOS simulator](https://docs.expo.dev/workflow/ios-simulator/)
- [Expo Go](https://expo.dev/go), a limited sandbox for trying out app development with Expo

You can start developing by editing the files inside the **app** directory. This project uses [file-based routing](https://docs.expo.dev/router/introduction).

## Get a fresh project

When you're ready, run:

```bash
npm run reset-project
```

This command will move the starter code to the **app-example** directory and create a blank **app** directory where you can start developing.

## Learn more

To learn more about developing your project with Expo, look at the following resources:

- [Expo documentation](https://docs.expo.dev/): Learn fundamentals, or go into advanced topics with our [guides](https://docs.expo.dev/guides).
- [Learn Expo tutorial](https://docs.expo.dev/tutorial/introduction/): Follow a step-by-step tutorial where you'll create a project that runs on Android, iOS, and the web.

## CI/CD

このプロジェクトは **EAS Workflows** を使用してCI/CDを構成しています。

### ブランチ戦略

| ブランチ | 用途 | 自動トリガー |
|---------|------|-------------|
| `main` | 本番環境 | productionビルド |
| `develop` | ステージング/テスト | previewビルド |
| `feature/*` | 機能開発 | 手動ビルドのみ |

### ワークフロー一覧

| ワークフロー | トリガー条件 | 実行内容 |
|-------------|-------------|---------|
| `preview-build.yml` | `develop`ブランチへプッシュ | Android/iOS のpreviewビルド作成 |
| `production-build.yml` | `main`ブランチへプッシュ | Android/iOS のproductionビルド作成 |
| `create-development-builds.yml` | 手動実行 | 開発用ビルド作成 |

### ビルドプロファイル (`eas.json`)

| プロファイル | 配布先 | チャネル | 用途 |
|-------------|-------|---------|------|
| `development` | internal | - | 開発者向け（デバッグ機能付き） |
| `development-simulator` | internal | - | iOSシミュレーター向け |
| `preview` | internal | `preview` | 内部テスター（TestFlight等） |
| `production` | store | `production` | App Store / Google Play |

### 開発フロー

```
1. feature/xxx ブランチで開発
2. develop にPRマージ → previewビルド自動作成 → 内部テスト
3. main にPRマージ → productionビルド自動作成 → ストア申請
```

### 手動ビルド

```bash
# 開発ビルド
eas build --profile development --platform all

# プレビュービルド
eas build --profile preview --platform all

# 本番ビルド
eas build --profile production --platform all

# ワークフロー実行
eas workflow:run create-development-builds
```

## Join the community

Join our community of developers creating universal apps.

- [Expo on GitHub](https://github.com/expo/expo): View our open source platform and contribute.
- [Discord community](https://chat.expo.dev): Chat with Expo users and ask questions.
