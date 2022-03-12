# Alembic Cheatsheet
### 1. Create alembic migration environment
```bash
alembic init alembic
```

### 2. Configure the migration environment
#### Editing the env.py file
The env.py script is part of the generated environment so that the way migrations run is entirely customizable.This is a Python script that is run whenever the alembic migration tool is invoked. At the very least, it contains instructions to configure and generate a SQLAlchemy engine, procure a connection from that engine along with a transaction, and then invoke the migration engine, using the connection as a source of database connectivity.
- SQLAlchemy url
- SQLAlchemy declarative base
<pre><code>
from logging.config import fileConfig
from sqlalchemy import engine_from_config
from sqlalchemy import pool
from alembic import context
<strong>
from app.models import Base
from app.config import settings
</strong>
# this is the Alembic Config object, which provides
# access to the values within the .ini file in use.
config = context.config
<strong>#override the sqlalchemy database url
config.set_main_option("sqlalchemy.url",settings.sqlalchemy_database_uri)</strong>
# Interpret the config file for Python logging.
# This line sets up loggers basically.
fileConfig(config.config_file_name)
# for 'autogenerate' support
# from myapp import mymodel
# target_metadata = mymodel.Base.metadata
<strong>target_metadata = Base.metadata<strong>
</code></pre>
Once these values are added, we can run a command to tell alembic our database exists and to start checking for migrations from this point forward:
```bash
alembic stamp head
```
An `alembic_version` table is created in the database to track the current version of our models.

### 3. Create a migration script
#### Method 1: Manual
```bash
alembic revision -m "migrations test"
```
This generates the migration script, the file contains some header information, identifiers for the current revision 
and a “downgrade” revision, an import of basic Alembic directives, and empty upgrade() and downgrade() functions. 
Then manually populate the upgrade() and downgrade() functions with directives that will apply a set of changes to our database. 
Typically, upgrade() is required while downgrade() is only needed if down-revision capability is desired, though it’s probably a good idea.

Example: 
```python
def upgrade():
    op.create_table(
        'test',
        sa.Column('id', sa.Integer, primary_key=True),
        sa.Column('name', sa.String(50), nullable=False),
        sa.Column('description', sa.Unicode(200)),
    )

def downgrade():
    op.drop_table('test')
```
#### Method 2: Autogenerating migrations
Populate revision script with candidate migration operations, based on comparison of database to model.
```bash
$ alembic revision --autogenerate -m "change made to models"
```
### 4. Run the migration
```bash
$ alembic upgrade head
```
### Relative Migration Identifiers
Relative upgrades/downgrades are also supported. To move two versions from the current, a decimal value “+N” can be supplied:
```bash
$ alembic upgrade +2
```
Negative values are accepted for downgrades:
```bash
$ alembic downgrade -1
```
Relative identifiers may also be in terms of a specific revision. For example, to upgrade to revision ae1027a6acf plus two additional steps:
```bash
$ alembic upgrade ae10+2
```
### Downgrading
Downgrade to last revision
```bash
$ alembic downgrade -1
```
Downgrade to the start
```bash
$ alembic downgrade base
```
