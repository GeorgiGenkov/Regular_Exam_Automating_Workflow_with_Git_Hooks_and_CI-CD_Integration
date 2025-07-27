## pre-commit:

#!/bin/sh

# Check code formatting

echo "Checking code formatting with Prettier..."
npx prettier --check .

if [ $? -ne 0 ]; then
echo "❌ Code is not formatted. Run 'npx prettier --write .' to fix."
exit 1
fi

echo "✅ Code formatting OK."

## pre-push
