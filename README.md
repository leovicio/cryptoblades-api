# Wax API

## Setup

Create a `.env` file with the following:

- `MONGODB_URI` - a ref to the mongodb instance
- `API_SECRET` - a string that must be passed for transactions to work

## Run

- `npm start` to start the API

## Routes

All routes that involve adding data take `secret` as a URL parameter. This must match `API_SECRET` (if set) or the request will fail.

### Getters

- GET `/static/leaderboard` - get the entire leaderboard
- GET `/static/characters/name/:id` - get character name by id
- GET `/static/weapons/name/:id` - get weapon name by id

### Transactions

Every endpoint additionally supports `gas` for logging and analytics purposes only.

#### Leaderboard
- GET `/leaderboard/fight/add` - pass `hash`, `accountAddress`, `characterId`, `characterLevel`, `weaponId`, `enemyId`, `wonFight`, `enemyRoll`, `playerRoll`, `xpGain`, `skillGain`
- GET `/leaderboard/weapon/mint/add` - pass `hash`, `accountAddress`, `weaponId`
- GET `/leaderboard/weapon/reforge/add` - pass `hash`, `accountAddress`, `weaponId`, `burnId`
- GET `/leaderboard/character/mint/add` - pass `hash`, `accountAddress`, `charId`
- GET `/leaderboard/character/level/add` - pass `hash`, `accountAddress`, `charId`, `level`
- GET `/leaderboard/market/list/add` - pass `hash`, `accountAddress`, `nftAddress`, `nftId`, `price`
- GET `/leaderboard/market/change/add` - pass `hash`, `accountAddress`, `nftAddress`, `nftId`, `price`
- GET `/leaderboard/market/sell/add` - pass `hash`, `accountAddress`, `buyerAddress`, `nftAddress`, `nftId`, `price`
- GET `/leaderboard/market/cancel/add` - pass `hash`, `accountAddress`, `nftAddress`, `nftId`

#### WAX
- GET `/wax/add` - pass `waxWallet`, `bscWallet` (optional), `waxAmount`, `waxChainTransactionId`, `waxChainBlockNumber`, `bscTransactionId` as URL parameters

#### Marketplace
- GET `/market/character` - pass `element` (string), `minLevel` (num), `maxLevel` (num), `sortBy` (string; any character key), `sortDir` (-1 or 1), `pageSize` (default 60), `pageNum` (default 0)
- PUT `/market/character/:charId` - pass `price`, (number), `charLevel` (num), `charElement` (string), `timestamp` (number), `sellerAddress` (string)
- GET `/market/character/:charId/sell` - mark this as sold (copy the entry from the market character collection)
- DELETE `/market/character/:charId` 
- GET `/market/weapon` - pass `element` (string), `minStars` (num), `maxStars` (num), `sortBy` (string; any weapon key), `sortDir` (-1 or 1), `pageSize` (default 60), `pageNum` (default 0)
- PUT `/market/weapon/:weaponId` - pass `price`, (string), `weaponStars` (num), `weaponElement` (string), `timestamp` (number), `sellerAddress` (string)
- GET `/market/weapon/:weaponId/sell` - mark this as sold (copy the entry from the market weapon collection)
- DELETE `/market/weapon/:weaponId` 