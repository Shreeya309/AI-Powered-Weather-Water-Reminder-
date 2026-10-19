AI-Powered Weather Water Reminder
HydraAI is a weather-aware hydration companion built with Expo, React Native, TypeScript, and an Express API. It helps users track their water intake, understand a daily hydration target, and receive contextual hydration tips.
Features
- Weather-aware hydration estimates: Uses weather conditions such as temperature and humidity, with UV information when available, to help estimate a daily water goal.
- Water intake tracking: Log drinks and review daily progress.
- Progress insights: View recent trends, streaks, and achievement badges.
- Custom reminders: Configure reminder intervals and quiet hours. Device notifications are opt-in and require permission.
- AI hydration tips: Request a contextual tip based on current weather and hydration progress.
- On-device preferences: Profile details, drink history, location choice, and reminder preferences are stored locally on the device.
The hydration target is calculated by the app using its configured inputs; the AI feature provides a coaching tip and does not set or override the target.
Tech Stack
- Mobile: Expo, React Native, Expo Router, TypeScript
- API: Node.js and Express 5
- Weather data: OpenWeatherMap
- AI tips: OpenAI API, accessed through the backend
- Local persistence: AsyncStorage
- Workspace and packages: pnpm monorepo
Project Structure
- artifacts/hydra-ai/app/ — mobile application
- artifacts/hydra-ai/context/HydrationContext.tsx — hydration profile, drink log, and reminder state
- artifacts/hydra-ai/lib/hydration.ts — hydration goal and progress calculations
- artifacts/api-server/src/routes/weather.ts — weather and city-search API routes
- artifacts/api-server/src/routes/hydration.ts — AI hydration insight route
- lib/api-spec/openapi.yaml — API contract source of truth
Requirements
- Node.js 24 or a version compatible with the workspace configuration
- pnpm
- API credentials for the external services used by the app
Configuration
Set these environment secrets for the API server in your development environment:
- OPENAI_API_KEY — used for AI hydration tips
- OPENWEATHERMAP_API_KEY — used to retrieve weather information
Keep API keys in server-side environment secrets. Do not commit real keys to the repository or expose them in the mobile client.
Run Locally
Install the workspace dependencies from the repository root:
pnpm install
Start the API server:
pnpm --filter @workspace/api-server run dev
In a separate terminal, start the Expo application:
pnpm --filter @workspace/hydra-ai run dev
Follow the Expo output to open the app in a supported simulator or device. Configure the API base URL as required by your local environment.
Type Checking
Check the mobile app:
pnpm --filter @workspace/hydra-ai run typecheck
Check the API server:
pnpm --filter @workspace/api-server run typecheck
Notes and Limitations
- Device reminders require notification permission and should be tested on a supported device. Notifications may not behave the same in a browser preview.
- UV information may be unavailable depending on the weather API plan or response; temperature and humidity can still be used when UV data is missing.
- AI tips require a valid server-side OpenAI API key and network access.
- Hydration estimates are general informational guidance, not medical advice. Individual hydration needs can vary.
Security and Privacy
The app is designed to keep profile details, selected location, reminder preferences, and drink history on the device. Weather requests and AI-tip requests are sent to the backend when needed. Review the implementation and your deployment configuration before publishing, and never commit API credentials.
Development Status
This repository contains a project under active development. Verify the app on a physical device and test API integrations, permissions, and error handling before using it in production.
