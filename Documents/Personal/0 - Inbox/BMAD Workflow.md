@bmad:bmm:workflows:create-story
@bmad:bmm:workflows:story-context
@bmad:bmm:workflows:story-ready
@bmad:bmm:workflows:dev-story
@bmad:bmm:workflows:story-done

![[Screenshot 2025-12-01 at 8.20.30 AM.png]]

Setup this 

UPSTASH_REDIS_REST_URL=
UPSTASH_REDIS_REST_TOKEN=


import { db } from "@arch-visual/db";
import {
	account,
	accountRelations,
	session,
	sessionRelations,
	user,
	userRelations,
	verification,
} from "@arch-visual/db/schema/auth";
import { checkout, polar, portal } from "@polar-sh/better-auth";
import { type BetterAuthOptions, betterAuth } from "better-auth";
import { drizzleAdapter } from "better-auth/adapters/drizzle";
import { nextCookies } from "better-auth/next-js";
import { polarClient } from "./lib/payments";

export const auth = betterAuth<BetterAuthOptions>({
	database: drizzleAdapter(db, {
		provider: "pg",

		schema: {
			account,
			accountRelations,
			session,
			sessionRelations,
			user,
			userRelations,
			verification,
		},
	}),
	trustedOrigins: [process.env.CORS_ORIGIN || ""],
	emailAndPassword: {
		enabled: true,
	},
	plugins: [
		polar({
			client: polarClient,
			createCustomerOnSignUp: true,
			enableCustomerPortal: true,
			use: [
				checkout({
					products: [
						{
							productId: "f6c3026e-2ed0-41ee-9f3c-d394bd9b38a6",
							slug: "100 credits",
						},
					],
					successUrl: process.env.POLAR_SUCCESS_URL,
					authenticatedUsersOnly: true,
				}),
				portal(),
			],
		}),
		nextCookies(),
	],
});


1. Run @bmad/bmm/workflows/create-story to generate detailed implementation plans for individual stories (e.g., 10.1, 10.3)

2. Run @bmad/bmm/workflows/sprint-planning to organize stories into sprints





create-story
validate-create-story
dev-story