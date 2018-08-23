���� [���ٿ�ʼ](./quickstart.md)

# Ŀ¼

* [Ŀ¼](#Ŀ¼)
* [��ѡ����](#��ѡ����)
    * [����Դ����](#����Դ����)
* [��ѡ��������](#��ѡ��������)
    * [ָ�����ɵı�](#ָ�����ɵı�)
    * [ָ������·��](#ָ������·��)
    * [ָ�����������ڵİ���](#ָ�����������ڵİ���)
    * [ָ������������](#ָ������������)
    * [ָ������xml���Ʋ���](#ָ������xml���Ʋ���)
    * [`paameterType`����](#`paametertype`����)
    * [ע������](#ע������)
    * [����ָ����������](#����ָ����������)
    * [�����ر���־](#�����ر���־)
    * [ָ�������ļ����·��](#ָ�������ļ����·��)


#��ѡ����

## ����Դ����

 ���ݿ����� `DB_DRIVER`
 ���ݿ����� `DB_URL`
 ��ռ� ���ݿ���  `DB_TABLE_SCHEMA`
 ���ݿ��û��� `DB_USERNAME`
 ���ݿ����� `DB_PASSWORD`
 ���ݿ����� `DB_TYPE`

`mysql`���ݿ�����

```properties
DB_TYPE=MYSQL
DB_DRIVER=com.mysql.cj.jdbc.Driver
DB_URL=jdbc:mysql://localhost:3306/
DB_TABLE_SCHEMA=test
DB_USERNAME=root
DB_PASSWORD=root
```
 `ORACLE`���ݿ�����

```properties
DB_TYPE=ORACLE
DB_DRIVER=oracle.jdbc.driver.OracleDriver
DB_URL=jdbc:oracle:thin:@192.168.0.1:1521:test
DB_TABLE_SCHEMA=test
DB_USERNAME=root
DB_PASSWORD=root
```

# ��ѡ��������

## ָ�����ɵı�

```properties
# ���ű���Ӣ�Ķ��Ÿ���,��Сд������,��������Ĭ��ΪDB_TABLE_SCHEMA�µ�ȫ����
DB_INCLUDE_TABLE_NAME=�����ɵı���1,�����ɵı���2
```
## ָ������·��

```properties
# �����ļ����·�� ��������Ĭ��Ϊ [��ǰ��Ŀ·��] ·����ʹ��/ ��\\�ָ� ����ʹ��/
FILE_OUT_PUT_PATH=C:/Users/admin/Desktop
```
## ָ�����������ڵİ���

```properties
# �����ļ��Ĺ������� ��������Ĭ���޹�����
BASE_PACKAGE=com.github.generator
# MAPPER���� �������� MAPPER���ڰ�·��Ϊ {BASE_PACKAGE}.dao
DAO_PACKAGE=dao
# POJO���� �������� POJO���ڰ�·��Ϊ {BASE_PACKAGE}.pojo
POJO_PACKAGE=pojo
# XML���� �������� XML�ļ����ڰ�·��Ϊ {BASE_PACKAGE}.xml
XML_PACKAGE=xml
```

## ָ������������

```properties
# ʵ������ Ĭ������ �շ����� {0}
POJO_NAME_FORMAT={0}
# MAPPER ���� Ĭ������ �շ����� + Dao {0}Dao
DAO_NAME_FORMAT={0}Dao
```

###### ����`java`������֧��3�����ã���`POJO_NAME_FORMAT`Ϊ�����������ݿ����Ϊ`test_user`

1. ȡ���ݿ������תΪ�շ����� �����������ɵ�`POJO`����Ϊ`TestUser`

   ```properties 
   POJO_NAME_FORMAT={0}
   ```

2. ȡ���ݿ������תΪ�շ����������ָ����ǰ��׺�������������ɵ�`POJO`����Ϊ`TestUserPOJO`

   ```properties
   POJO_NAME_FORMAT={0}POJO
   ```

3. ָ������ �����������ɵ�`POJO`����Ϊ`User` , �����ڵ�������

   ```properties
   POJO_NAME_FORMAT= User
   ```

## ָ������xml���Ʋ���

```properties
# XML ���� Ĭ�ϱ�����Сд  ��CAMEL ��Ĭ��Ϊ������Сд
# ֧���������� 
# Ĭ�� TABLE_NAME_LOWERCASE ������Сд
XML_NAME_FORMAT=TABLE_NAME_LOWERCASE
# ������ת�շ�
# XML_NAME_FORMAT=CAMEL
```

`paameterType`����



## `paameterType`����

 XML��`parameterType` �Ƿ�ʹ�ñ��� Ĭ��Ϊ`false`
 ����`POJO`ȫ·��Ϊ `test.generator.pojo.UserBean`
` PARAMETER_TYPE_USE_TYPE_ALIASES=false` �� ȡ`POJO`����ȫ�޶��� :
` parameterType="test.generator.pojo.UserBean"`
` PARAMETER_TYPE_USE_TYPE_ALIASES=true` �� ȡ`POJO`����������ĸСдΪ���� :
 `parameterType="userBean"`

```properties
PARAMETER_TYPE_USE_TYPE_ALIASES=false
```
## ע������


```properties
# ���� �����ô�����Ĭ�ϲ�����@authorע����Ϣ
AUTHOR=TODO
# �����汾�� �����ô�����Ĭ�ϲ�����@sinceע����Ϣ
SINCE_VERSION=1.0
#��ǰ�汾�� �����ô���Ĭ��1.0
VERSION=1.0
```
## ����ָ����������

```properties
# ��������   Ĭ��Ϊtrue
INSERT_METHOD_ENABLED=true
# ���ݴ������ɾ������   Ĭ��Ϊtrue
DELETE_METHOD_ENABLED=true
# ��������ɾ������  Ĭ��Ϊtrue �����δ�������������ɴ˷���
DELETE_BY_PRIMARY_KEY_METHOD_ENABLED=true
# ����������������  Ĭ��Ϊtrue �����δ�������������ɴ˷���
UPDATE_BY_PRIMARY_KEY_METHOD_ENABLED=true
# ���ݴ��������ѯ�����б�   Ĭ��Ϊtrue
QUERY_METHOD_ENABLED=true
# ����������ѯ���� Ĭ��Ϊtrue �����δ�������������ɴ˷��� 
QUERY_BY_PRIMARY_KEY_ENABLED=true
# ͳ�Ʒ�����������������   Ĭ��Ϊtrue
COUNT_METHOD_ENABLED=true
```

## �����ر���־

```properties
#�Ƿ�������־ Ĭ�Ͽ���
LOG_ENABLED=true
```

## ָ�������ļ����·��

> ���ó���: ������������ָ��λ��(��������)ʱ,Ϊ�˼���·���㼶,��ָ���ļ�·��,�����ò�Ӱ�����������ڵİ��ṹ

 �粻ָ�����·��,��Ĭ�����·��Ϊ: `{FILE_OUT_PUT_PATH}/{BASE_PACKAGE}/{���������ڵİ���}`
 ָ���ļ����·�������ļ����·��Ϊ׼. �ļ����·��֧��`���·��`


```properties
# xml�ļ����·�� �������� �������·��Ϊ {FILE_OUT_PUT_PATH}/xml
XML_OUT_PUT_PATH=xml
# mapper�ļ����·�� �������� �������·��Ϊ {FILE_OUT_PUT_PATH}/dao
DAO_OUT_PUT_PATH=/dao
# pojo�ļ����·�� �������� �������·��Ϊ {FILE_OUT_PUT_PATH}/MultiCatalog/pojo
POJO_OUT_PUT_PATH=MultiCatalog/pojo
```
