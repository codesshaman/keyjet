#!/bin/bash

set -euo pipefail

USER_NAME="$(whoami)"
HOST_NAME="$(hostname -f 2>/dev/null || hostname)"

# Имя ключа
KEY_NAME="gitlab_deploy"

KEY_PATH="$HOME/.ssh/$KEY_NAME"
COMMENT="${USER_NAME}@${HOST_NAME}"

mkdir -p "$HOME/.ssh"
chmod 700 "$HOME/.ssh"

if [[ -f "$KEY_PATH" ]]; then
    echo "Ключ уже существует: $KEY_PATH"
    read -r -p "Перезаписать ключ? [y/N]: " answer
    
    case "$answer" in [yY]|[yY][eE][sS])
        echo "Перезаписываю ключ..." rm -f "$KEY_PATH" "${KEY_PATH}.pub"
        ;;
    *)
        echo "Операция отменена."
        exit 0
        ;;
    esac
fi

echo "Создаю GitLab Deploy Key:"
echo "  User: $USER_NAME"
echo "  Host: $HOST_NAME"
echo "  Name: $KEY_NAME"
echo "  Key:  $KEY_PATH"
echo

ssh-keygen \
    -t ed25519 \
    -C "$COMMENT" \
    -f "$KEY_PATH" \
    -N ""

echo
echo "=== GitLab Deploy Key ==="
cat "${KEY_PATH}.pub"
echo
