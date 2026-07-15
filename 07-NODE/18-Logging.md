🔹 Logging
Never use console.log for production logging. It blocks the process because it is synchronous when writing to standard output. Instead, use a structured logging library like Winston or Pino.

JavaScript
const winston = require('winston');

const logger = winston.createLogger({
level: 'info',
format: winston.format.json(),
transports: [
new winston.transports.File({ filename: 'logs/error.log', level: 'error' }),
new winston.transports.File({ filename: 'logs/combined.log' }),
],
});

// Production log writing
logger.error('❌ Connection to cache cluster failed.');
logger.info('✅ Database sync complete.');
