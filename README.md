# Använd Drizzle med TanStack Start

I den här uppgiften ska du **lära dig grunderna i Drizzle ORM** genom att skapa en enkel app med **TanStack Start** som backend och frontend.  
Du ska spara, läsa och visa data från en **SQLite-databas** via Drizzle.

---

## 🎯 Mål

Efter uppgiften ska du kunna:

- Skapa och koppla en Drizzle-databas i TanStack Start
- Skapa tabeller och lägga till data
- Läsa data med serverfunktioner och visa det i UI:t
- Förstå grunderna i hur ORM och SQL hänger ihop

---

## 🧰 Förberedelser

Skapa ett nytt tanstack projekt och installera drizzle:

```bash
npm create @tanstack/start@latest my-drizzle-app --add-ons tanstack-query
cd my-drizzle-app
npm install drizzle-orm better-sqlite3
npm install -D drizzle-kit
```

---

## 🗄️ Steg 1: Skapa en databas och tabell

Skapa en mapp `db/` och en fil `schema.ts`.  
Definiera en enkel tabell `notes` med följande kolumner:

- `id` (autoincrement, primary key)
- `title` (text)
- `content` (text)
- `createdAt` (datum)

Skapa sedan en `db.ts` som:

- Initierar `better-sqlite3`
- Använder `drizzle()` för att skapa en db-instans

se steg2 här [https://orm.drizzle.team/docs/get-started-sqlite#better-sqlite3](https://orm.drizzle.team/docs/get-started-sqlite#better-sqlite3)

👉 Lägg till hjälpfunktioner i `db.ts` för att:

- `getNotes()` → returnerar alla anteckningar
- `addNote()` → lägger till en ny anteckning

---

## Steg 2: Koppla Drizzle till TanStack Start

Skapa en **server function** i `app/routes/api/notes.ts` som:

- Vid `GET` → hämtar alla anteckningar från `getNotes()`
- Vid `POST` → tar emot `title` och `content` från `request` och lägger till en anteckning via `addNote()`

---

## Steg 3: Visa datan i UI:t

Skapa en route `app/routes/notes.tsx` som:

- Hämtar anteckningar med `useSuspenseQuery` via `ensureQueryData`
- Visar listan av anteckningar i en enkel `<ul>`

---

## Steg 4: Lägg till nya anteckningar

Lägg till ett enkelt `<form>` med två inputs:

- `title`
- `content`

Använd `useMutation` för att skicka POST-request till din `/api/notes`-route.  
Efter lyckad mutation → `invalidate` queryn så listan uppdateras.
