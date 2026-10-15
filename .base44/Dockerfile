# Runtime image for the Base44 sandbox stack.
#
# Plain Node runtime plus the pnpm version pinned by the root `packageManager`
# field, so no source is baked into the image and every service runs the
# bind-mounted working tree.
FROM node:22

RUN npm install -g pnpm@11.27.0

# Keep the store inside the bind-mounted workspace, so installs hardlink instead of
# copying across filesystems, and keep `pnpm exec` off the registry: the `setup`
# service has already installed the workspace before `web` starts.
RUN pnpm config set store-dir /app/.pnpm-store --location=global \
	&& pnpm config set verify-deps-before-run false --location=global
