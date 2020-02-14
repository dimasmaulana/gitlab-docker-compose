# GitLab Docker Compose Configuration

This file defines a Docker Compose configuration for running a GitLab CE instance.

## Version

* `version: '3.6'`

## Services

* **web:**
    * **Image:** `gitlab/gitlab-ce:$GITLAB_VERSION` - Uses the official GitLab CE Docker image.
    * **Restart:** `always` - Ensures the container restarts automatically if it stops.
    * **Hostname:** `'$GITLAB_HOST'` - Sets the hostname for the GitLab instance.
    * **Environment:**
        * **`GITLAB_OMNIBUS_CONFIG`:**  A multi-line variable containing GitLab configuration options.
            * **`external_url`:** Sets the external URL for the GitLab instance.
            * **`letsencrypt['enable']`:** Enables Let's Encrypt for SSL certificates.
            * **`gitlab_rails['smtp_enable']`:** Enables SMTP for email notifications.
            * **`gitlab_rails['smtp_address']`, `gitlab_rails['smtp_port']`, `gitlab_rails['smtp_user_name']`, `gitlab_rails['smtp_password']`, `gitlab_rails['smtp_domain']`, `gitlab_rails['smtp_authentication']`, `gitlab_rails['smtp_enable_starttls_auto']`, `gitlab_rails['smtp_openssl_verify_mode']`:** Configure SMTP settings.
            * **`gitlab_rails['gitlab_email_from']`, `gitlab_rails['gitlab_email_reply_to']`:** Set the sender email address for GitLab.
            * **`gitlab_rails['incoming_email_enabled']`, `gitlab_rails['incoming_email_address']`, `gitlab_rails['incoming_email_email']`, `gitlab_rails['incoming_email_password']`, `gitlab_rails['incoming_email_host']`, `gitlab_rails['incoming_email_port']`, `gitlab_rails['incoming_email_ssl']`, `gitlab_rails['incoming_email_mailbox_name']`, `gitlab_rails['incoming_email_idle_timeout']`, `gitlab_rails['incoming_email_delete_after_delivery']`, `gitlab_rails['incoming_email_expunge_deleted']`:** Configure incoming email settings.
            * **`puma['worker_processes']`:** Sets the number of Puma worker processes.
            * **`sidekiq['max_concurrency']`:** Sets the maximum number of concurrent Sidekiq jobs.
            * **`prometheus_monitoring['enable']`:** Disables Prometheus monitoring.
    * **Ports:**
        * **`'$PORT_HTTP:80'`:** Exposes port 80 for HTTP traffic.
        * **`'$PORT_HTTPS:443'`:** Exposes port 443 for HTTPS traffic.
        * **`'$PORT_SSH::22'`:** Exposes port 22 for SSH access.
    * **Volumes:**
        * **`'$GITLAB_HOME/config:/etc/gitlab'`:** Mounts a volume for the GitLab configuration files.
        * **`'$GITLAB_HOME/logs:/var/log/gitlab'`:** Mounts a volume for the GitLab logs.
        * **`'$GITLAB_HOME/data:/var/opt/gitlab'`:** Mounts a volume for the GitLab data.
    * **`shm_size: '256m'`:** Sets the shared memory size for the container.

## Notes

* Replace the placeholder variables (`$GITLAB_VERSION`, `$GITLAB_HOST`, `$GITLAB_EXTERNAL_URL`, `$SMTP_HOST`, `$SMTP_PORT`, `$EMAIL_USER`, `$EMAIL_PASS`, `$SMTP_DOMAIN`, `$GITLAB_EMAIL`, `$GITLAB_EMAIL_REPLY_TO`, `$GITLAB_INCOMING_EMAIL_ADDRESS`, `$IMAP_PORT`, etc.) with your actual values.
* This configuration assumes you have a volume named `$GITLAB_HOME` mounted in your Docker Compose environment.

## License

This project is licensed under the [MIT License](LICENSE).

