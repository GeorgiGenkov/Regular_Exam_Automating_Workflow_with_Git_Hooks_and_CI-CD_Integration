## pre-commit:

#!/bin/sh

echo "Checking code formatting with Prettier..."
npx prettier --check .

if [ $? -ne 0 ]; then
echo "❌ Code is not formatted. Run 'npx prettier --write .' to fix."
exit 1
fi

echo "✅ Code formatting OK."

## pre-push:

#!/bin/sh

echo "Running unit tests..."
npm test

if [ $? -ne 0 ]; then
echo "❌ Tests failed. Push blocked."
exit 1
fi

echo "✅ Tests passed. Push allowed."

## prepare-commit-msg:

#!/bin/sh

commit_msg=$(cat "$1")
pattern="^TASK-[0-9]+: "

if ! echo "$commit_msg" | grep -qE "$pattern"; then
echo "❌ Commit message must match pattern: TASK-123: Fix something"
exit 1
fi

echo "✅ Commit message format OK."
