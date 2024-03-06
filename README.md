# `supabase-grafana`

Observability for your Supabase project, using Prometheus/Grafana, collecting [~200 metrics](./docs/metrics.md):

![./docs/supabase-grafana.png](./docs/supabase-grafana.png)

## Getting started

To run the collector locally using Docker Compose:

### Create secrets

Create an `.env` file:

```
cp .env.example .env
```

Fill it out with your project details. You'll need your project ref and service role key, which you can find [here](https://app.supabase.com/project/_/settings/api).
Alternatively, to monitor multiple projects you'll need to create an access token [here](https://supabase.com/dashboard/account/tokens).

### Run with Docker

After that, simply start docker compose and you will be able to access Grafana:

```
docker compose up
```

### Access the dashboard

![./docs/supabase-grafana-prometheus.png](./docs/supabase-grafana-prometheus.png)

Visit [localhost:8000](https://localhost:8000) and login with the credentials:

- Username: `admin`
- Password: [the password in your `.env` file]

## Deploying

Deploy this service to a server which is always running to continuously collect metrics for your Supabase project.

### Using Fly.io

You can run the collector on a free instance of [Fly.io](https://fly.io/)

Follow these steps:

1. Make sure you have the [Fly CLI](https://fly.io/docs/getting-started/installing-flyctl/) installed, and you are logged in.
2. Run `fly launch` to deploy the app to Fly.
3. Copy your `.env` file to your Fly project: `fly secrets import < .env`
4. After a successful deployment, your app will be available at `https://<your-app-name>.fly.dev`

### Using Caprover for self-hosting

You can also run the collector on your own server using [Caprover](https://caprover.com/).

Follow these steps:

1. Create a new app on Caprover with persistent data. <br>
   Optional:
   - Set container http port to 8080.
   - Enable HTTPS and force redirect.
2. Copy your `.env` file to your Caprover app configuration.
3. Add persistent storage for the `/data` directory.
4. Deploy the app.
