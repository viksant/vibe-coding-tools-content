---
title: "Database Migration Builder"
description: "Create safe, reversible database migrations with proper rollback strategies"
category: "template-prompt"
tags: ["database", "migration", "schema-change", "rollback", "data-migration"]
tech_stack: ["postgresql", "mysql", "mongodb", "django", "rails", "knex"]
---

# Database Migration Builder

You are a database expert specializing in safe, reversible database migrations.

## Migration Requirements
- **Database Type**: [INSERT DATABASE - PostgreSQL, MySQL, SQLite, MongoDB]
- **Migration Tool**: [INSERT TOOL - Django, Rails, Knex, Flyway, Liquibase]
- **Change Type**: [INSERT TYPE - schema, data, index, constraint]
- **Risk Level**: [INSERT RISK - low, medium, high, critical]
- **Rollback Required**: [INSERT REQUIREMENT - yes/no]
- **Data Volume**: [INSERT SIZE - small, medium, large dataset]

## Migration Details
[INSERT SPECIFIC MIGRATION REQUIREMENTS AND CURRENT SCHEMA]

## Output Format

### Migration Script

```sql
-- Migration: [MIGRATION_NAME]
-- Version: [VERSION_NUMBER]
-- Description: [MIGRATION_PURPOSE]
-- Author: [AUTHOR]
-- Date: [DATE]

-- ==============================================
-- PRE-MIGRATION CHECKS
-- ==============================================

-- Check current database version
DO $$
BEGIN
    IF NOT EXISTS (
        SELECT 1 FROM information_schema.tables 
        WHERE table_name = 'schema_migrations'
    ) THEN
        RAISE EXCEPTION 'Schema migrations table not found';
    END IF;
END $$;

-- Verify prerequisites
[PREREQUISITE_CHECKS]

-- ==============================================
-- BACKUP RECOMMENDATIONS
-- ==============================================

-- Run these commands before migration:
-- pg_dump [database] > backup_before_[migration_name].sql
-- [DATABASE_SPECIFIC_BACKUP_COMMANDS]

-- ==============================================
-- MIGRATION - FORWARD
-- ==============================================

BEGIN;

-- Step 1: [STEP_DESCRIPTION]
[SQL_STATEMENTS]

-- Step 2: [STEP_DESCRIPTION]
[SQL_STATEMENTS]

-- Add migration record
INSERT INTO schema_migrations (version, applied_at) 
VALUES ('[VERSION_NUMBER]', NOW());

COMMIT;

-- ==============================================
-- POST-MIGRATION VALIDATIONS
-- ==============================================

-- Verify data integrity
[VALIDATION_QUERIES]

-- Check constraints
[CONSTRAINT_CHECKS]

-- Performance checks
[PERFORMANCE_VALIDATIONS]
```

### Rollback Script

```sql
-- Rollback: [MIGRATION_NAME]
-- Version: [VERSION_NUMBER]
-- Description: Rollback [MIGRATION_PURPOSE]

-- ==============================================
-- PRE-ROLLBACK CHECKS
-- ==============================================

-- Verify migration was applied
DO $$
BEGIN
    IF NOT EXISTS (
        SELECT 1 FROM schema_migrations 
        WHERE version = '[VERSION_NUMBER]'
    ) THEN
        RAISE EXCEPTION 'Migration [VERSION_NUMBER] was not applied';
    END IF;
END $$;

-- Check for dependent data
[DEPENDENCY_CHECKS]

-- ==============================================
-- ROLLBACK - REVERSE
-- ==============================================

BEGIN;

-- Step 1: [REVERSE_STEP_DESCRIPTION]
[REVERSE_SQL_STATEMENTS]

-- Step 2: [REVERSE_STEP_DESCRIPTION]
[REVERSE_SQL_STATEMENTS]

-- Remove migration record
DELETE FROM schema_migrations 
WHERE version = '[VERSION_NUMBER]';

COMMIT;

-- ==============================================
-- POST-ROLLBACK VALIDATIONS
-- ==============================================

-- Verify rollback success
[ROLLBACK_VALIDATIONS]
```

### Framework-Specific Implementation

#### Django Migration
```python
# migrations/[number]_[migration_name].py
from django.db import migrations, models
import django.db.models.deletion

class Migration(migrations.Migration):
    dependencies = [
        ('[app_name]', '[previous_migration]'),
    ]

    operations = [
        migrations.CreateModel(
            name='[ModelName]',
            fields=[
                ('id', models.AutoField(primary_key=True)),
                ('[field_name]', models.[FieldType]([field_options])),
            ],
            options={
                'db_table': '[table_name]',
                'indexes': [
                    models.Index(fields=['[field]'], name='[index_name]'),
                ],
            },
        ),
        
        # Data migration
        migrations.RunPython(
            code=migrate_data_forward,
            reverse_code=migrate_data_reverse,
        ),
    ]

def migrate_data_forward(apps, schema_editor):
    """Migrate data forward"""
    [ModelName] = apps.get_model('[app_name]', '[ModelName]')
    
    # Data migration logic
    [DATA_MIGRATION_FORWARD]

def migrate_data_reverse(apps, schema_editor):
    """Migrate data backward"""
    [ModelName] = apps.get_model('[app_name]', '[ModelName]')
    
    # Reverse data migration logic
    [DATA_MIGRATION_REVERSE]
```

#### Rails Migration
```ruby
# db/migrate/[timestamp]_[migration_name].rb
class [MigrationName] < ActiveRecord::Migration[6.1]
  def up
    create_table :[table_name] do |t|
      t.[type] :[field_name], [options]
      t.timestamps
    end
    
    add_index :[table_name], :[field_name]
    
    # Data migration
    [DataMigrationForward]
  end

  def down
    # Reverse data migration
    [DataMigrationReverse]
    
    drop_table :[table_name]
  end
  
  private
  
  def [data_migration_method]
    # Data migration logic
  end
end
```

### Data Migration Strategy

```sql
-- Large dataset migration approach
-- Use batching for large tables

DO $$
DECLARE
    batch_size INT := 1000;
    offset_val INT := 0;
    total_rows INT;
    processed_rows INT := 0;
BEGIN
    -- Get total count
    SELECT COUNT(*) INTO total_rows FROM [source_table];
    
    RAISE NOTICE 'Starting migration of % rows', total_rows;
    
    LOOP
        -- Process batch
        WITH batch AS (
            SELECT * FROM [source_table]
            WHERE [conditions]
            LIMIT batch_size OFFSET offset_val
        )
        UPDATE [target_table] 
        SET [field] = [transformation]
        FROM batch
        WHERE [join_condition];
        
        -- Check if we're done
        GET DIAGNOSTICS processed_rows = ROW_COUNT;
        offset_val := offset_val + batch_size;
        
        RAISE NOTICE 'Processed % of % rows', offset_val, total_rows;
        
        EXIT WHEN processed_rows < batch_size;
        
        -- Commit batch to avoid long-running transaction
        COMMIT;
    END LOOP;
    
    RAISE NOTICE 'Migration completed successfully';
END $$;
```

### Migration Testing

```sql
-- Test migration on copy of production data
-- 1. Create test database
CREATE DATABASE [test_database];

-- 2. Restore production backup
-- pg_restore -d [test_database] [backup_file]

-- 3. Run migration
\i [migration_file.sql]

-- 4. Verify results
[VERIFICATION_QUERIES]

-- 5. Test rollback
\i [rollback_file.sql]

-- 6. Verify rollback
[ROLLBACK_VERIFICATION_QUERIES]
```

### Performance Monitoring

```sql
-- Monitor migration progress
SELECT 
    schemaname,
    tablename,
    n_tup_ins as inserts,
    n_tup_upd as updates,
    n_tup_del as deletes
FROM pg_stat_user_tables 
WHERE tablename = '[table_name]';

-- Check for blocking queries
SELECT 
    pid,
    query,
    state,
    query_start,
    state_change
FROM pg_stat_activity 
WHERE state != 'idle';
```

### Migration Checklist

#### Pre-Migration
- [ ] Database backup completed
- [ ] Migration tested on staging
- [ ] Rollback script prepared and tested
- [ ] Team notified of maintenance window
- [ ] Application scaled down if needed

#### During Migration
- [ ] Monitor migration progress
- [ ] Check for blocking queries
- [ ] Verify no data corruption
- [ ] Monitor system resources

#### Post-Migration
- [ ] Run validation queries
- [ ] Check application functionality
- [ ] Monitor performance metrics
- [ ] Update documentation
- [ ] Clean up temporary data

### Emergency Procedures

```bash
#!/bin/bash
# Emergency rollback script

echo "Starting emergency rollback..."

# 1. Stop application traffic
[STOP_APPLICATION_COMMANDS]

# 2. Execute rollback
psql -d [database] -f rollback_[migration_name].sql

# 3. Verify rollback
psql -d [database] -c "[VERIFICATION_QUERY]"

# 4. Restart application
[START_APPLICATION_COMMANDS]

echo "Emergency rollback completed"
```

## Success Criteria
- Migration completes without errors
- All data integrity maintained
- Performance impact minimal
- Rollback tested and working
- Application functionality preserved