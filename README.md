## Requirements and Prerequisites

1. Install postgresql in your environment without docker, install psql cli
2. Run postgresql 
3. Connect to postgres with psql cli
4. Create/Modify user postgres with a new password. ie fellowship for now, Create database fellowship.
5. Install nvm 
6. Install node with nvm. latest stable.



# Commands that are helpful

sudo -u postgres psql
show hba_file;
show config_file;


In postgresql.conf:

listen_addresses = 'localhost'


In pg_hba.conf
host    all     all     127.0.0.1/32    md5