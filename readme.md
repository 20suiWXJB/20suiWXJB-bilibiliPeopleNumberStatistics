初始化数据库结构
```sql
-- 表1：monitored_video (被监控的视频信息表)
CREATE TABLE monitored_video (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    bvid VARCHAR(255) NOT NULL UNIQUE,
    video_title VARCHAR(1024),
    up_name VARCHAR(255),
    is_active TINYINT NOT NULL DEFAULT 1,
    created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
);

-- 表2：video_stat_point (视频数据点表)
CREATE TABLE video_stat_point (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    video_id BIGINT NOT NULL,
    view_count INTEGER NOT NULL,
    like_count INTEGER,
    coin_count INTEGER,
    favorite_count INTEGER,
    timestamp TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (video_id) REFERENCES monitored_video (id) ON DELETE CASCADE
);

-- 为外键创建索引（H2 会自动为外键建索引，但显式创建更明确）
CREATE INDEX idx_video_id ON video_stat_point (video_id);
```