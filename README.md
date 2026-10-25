# Sylvara Guard Portal (starter)

Starter website for a Minecraft roleplay department: public home/rules pages, username/password login, on-duty report submission, member report history, and supervisor review.

## Important before public launch

- Replace sample Rules content with the official Sylvara Guard rules.
- Do not put real credentials, database IDs, or secrets in public files.
- This starter does not include self-service registration. Admins create accounts.
- Configure Cloudflare D1 and the `wrangler.toml` database ID before deployment.
- Review security, backups, retention, and access rules before using with real staff data.

## Requirements

Node.js 20+ and npm.

## Setup

1. Install dependencies: `npm install`
2. Create a D1 database: `npm run db:create`
3. Copy the returned database ID into `wrangler.toml` in place of `REPLACE_WITH_YOUR_D1_DATABASE_ID`.
4. Apply schema locally: `npm run db:migrate:local`
5. Apply schema remotely: `npm run db:migrate:remote`
6. Create the first user using `node scripts/create-user.mjs`. The script prints an SQL statement; execute it against the remote database with Wrangler D1. Keep the generated SQL private.
7. Test locally with `npm run dev`.
8. Deploy with `npm run deploy`.

## Add first user to remote D1

After creating the user with the script, run the printed INSERT statement with:

`npx wrangler d1 execute sylvara-guard-db --remote --command="PASTE INSERT SQL HERE"`

Do not paste a real password into a public repository or public issue.

## Routes

- `/` public home
- `/rules.html` public rules
- `/login.html` login
- `/dashboard.html` member dashboard
- `/report-new.html` submit on-duty report
- `/reports.html` personal report history
- `/review-reports.html` supervisor review
- `/api/*` backend routes

## Roles

- `member`: submit and view own reports
- `supervisor`: member permissions plus review reports
- `admin`: supervisor permissions plus view member list

The first admin must be created manually. There is no public endpoint for self-registering or granting privileges.
