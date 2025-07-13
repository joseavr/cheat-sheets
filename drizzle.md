

# Drizzle API

## Schemas


### Relational Schemas for Relational Queries


## Relational Query


## SQL-like Query


# Drizzle-Zod

Let's say we have the folloing schema

```ts
export const expenses = pgTable("expenses", 
	{
		id: serial("id").primaryKey(),
		userId: text("user_id").notNull(),
		title: text("title").notNull(),
		amount: numeric ("amount", { precision: 12, scale: 2 }) -notNull(),
		createdAt: timestamp ('created_at').defaultNow()
	},
	(expenses) => {
		return { userIdIndex: index("name_idx").on(expenses.userId) }
)
```

We can generate types for selecting, inserting, updating, deleting, before doing anything to the DB

```ts
import { createInsertSchema, createSelectSchema, createUpdateSchema } from "drizzle-zod"

// Schema for inserting a user - can be used to validate API requests
const insertExpenseSchema = createInsertSchema(expenses)
// Schema for selecting a Expenses - can be used to validate API responses
const selectExpensesSchema = createSelectSchema(expenses)
```

Tip: always parse the data before inserting, updating, deleting into the database. For example:

```ts
// throws an error if not valid
const validatedExpense = insertExpenseSchema.parse({
	...expense,
	userId: user.id,
})

const result = await db.insert(expenseTable).values(validatedExpense)
```

Tip: previous are scenarios in the backend, how about in the frontend? Best practice to parse with zod with another Schema that derives from the backedn zod schema. For example:

```ts
// BACKEND schema
export const insertExpenseSchema = createInsertSchema(expenses, {
	title: z.string().min(3, { message: "Title must be at least 3 characters" }),
	amount: z.string().regex(/^\d+(\.\d{1,2})?$/, { message: "Amount must be postive"})
})

// FRONTEND, shared schema that can be used in the frontend
const createExpenseSchema = insertExpenseSchema.omit({ 
	userId: true, 
	createdAt: true 
})

const validatedExpense = createExpenseSchema.parse({
	...expense,
	userId: user.id,
})
// -> should throw since we passing `userId`
```

## Validating request as middleware in Hono

```ts
.post("/", zValidator("json", createPostSchema), async (c) => {
	const data = await c.req.valid("json") // zod parses and data stored at valid()
	const expense = createPostSchema.parse(data)

	return c. json (expense) ;
})
```