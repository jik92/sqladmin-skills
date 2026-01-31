# File and image fields

SQLAdmin integrates with `fastapi-storages` to handle file uploads.

## Typical pattern
- Install `fastapi-storages` and the backend you want (e.g., filesystem or S3).
- Define a storage instance.
- Use `FileType` or `ImageType` in your SQLAlchemy model.

Example outline:

```python
from fastapi_storages import FileSystemStorage
from fastapi_storages.integrations.sqlalchemy import FileType, ImageType

storage = FileSystemStorage(path="./uploads")

class Asset(Base):
    __tablename__ = "assets"
    id = Column(Integer, primary_key=True)
    file = Column(FileType(storage=storage))
    image = Column(ImageType(storage=storage))
```

Use S3 or other backends by swapping the storage class and settings.
