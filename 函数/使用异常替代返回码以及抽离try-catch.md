### bad case
```java
if (deletePage(page) == E_ok) {
  if (registry.deleteReference(page.name) == E_ok) {
    if (configKeys.deleteKey(page.name.makekEY()) == E_ok) {
      logger.log("page deleted");
    } else {
      logger.log("configKey not delete");
    }
  } else {
    logger.log("deleteReference from registry failed");
  }
} else {
  logger.log("delete failed");
  retun E_Error;
}
```

### better case
```java
try{
  deletePage(page);
  registry.deleteReference(page.name);
  configKeys.deleteKey(page.name.makeKey());
}
catch (Exception e) {
  logger.log(e.getMessage());
}
```

### best case
```java
// delete 函数只与错误处理有关，很容易理解然后忽略掉
public void delete(Page page) {
  try {
    deletePageAndAllReferences(page);
  }
  catch (Excetion e) {
    logError(e);
  }
}

// deletepAndAllReferences 删除只与完全删除一个page有关，错误处理可以忽略掉
private void deletepAndAllReferences(Page page) throws Exception {
  deletePage(page);
  registry.deleteReference(page.name);
  configKeys.deleteKey(page.name.makeKey());
}

private void logError(Excetion e) {
  logger.log(e.getMessage());
}
```