���� [���ٿ�ʼ](./quickstart.md)

* [�߼�����](#�߼�����)
    * [�Զ��巽��ע��](#�Զ��巽��ע��)
    * [�Զ�������������](#�Զ�������������)
    * [�Զ���ӳ������](#�Զ���ӳ������)
    * [�Զ���������](#�Զ���������)


# �߼�����

## �Զ��巽��ע��

```java
import java.io.IOException;

import org.apache.ibatis.io.Resources;

import com.github.zhuyizhuo.generator.mybatis.convention.MethodCommentInfo;
import com.github.zhuyizhuo.generator.mybatis.generator.Generator;
import com.github.zhuyizhuo.generator.mybatis.generator.GeneratorBuilder;

public class TestGenerator {
    public static void main(String[] args) throws IOException {
        MethodCommentInfo methodCommentInfo = new MethodCommentInfo();
        //�޸�count����ע��
        methodCommentInfo.setCountMethodDescription(" count method description ");
        Generator generator = new GeneratorBuilder()
            .addMethodComment(methodCommentInfo)
            .build(Resources.getResourceAsStream("config.properties"));
        generator.generate();
    }
}
```

## �Զ�������������

�Զ������������ƺ󽫸��������ļ�����

- ֧���Զ������� `xml `���� (���Ƕ�Ӧ������ `XML_NAME_FORMAT`)
- ֧���Զ������� `pojo` ���� (���Ƕ�Ӧ������ `POJO_NAME_FORMAT`)
- ֧���Զ������� `mapper` ���� (���Ƕ�Ӧ������ `DAO_NAME_FORMAT`)

�˴���`�Զ������� xml ����`Ϊ��:

```java
import java.io.IOException;

import org.apache.ibatis.io.Resources;

import com.github.zhuyizhuo.generator.mybatis.extension.service.FormatService;
import com.github.zhuyizhuo.generator.mybatis.generator.Generator;
import com.github.zhuyizhuo.generator.mybatis.generator.GeneratorBuilder;

public class TestGenerator {
    //�Զ�������xml�ļ����� 
    public static void main(String[] args) throws Exception{
        Generator generator = new GeneratorBuilder()
            .addXmlNameFormat(new FormatService() {
            @Override
            public String formatTableName(String tableName) {
                //�˴�Ϊ���ݿ�����ƴ�д,�û��ɽ������Զ��崦��󷵻�
                System.out.println("���ݿ�����ƴ�д��" + tableName);
                return tableName + "_sql";
            }
        }).build(Resources.getResourceAsStream("config.properties"));
        generator.generate();
    }
}
```

`java8 ` lambda ���ʽ�÷�����:

```java
import java.io.IOException;

import org.apache.ibatis.io.Resources;

import com.github.zhuyizhuo.generator.mybatis.generator.Generator;
import com.github.zhuyizhuo.generator.mybatis.generator.GeneratorBuilder;
import com.github.zhuyizhuo.generator.utils.GeneratorStringUtils;

public class TestGenerator {
	
	public static void main(String[] args) throws IOException {
		Generator generator = new GeneratorBuilder()
				.addBeanNameFormat((tableName) ->{
                    System.out.println("���ݿ�����ƴ�д��" + tableName);
					//�Զ������ݿ�ӳ���������
					return GeneratorStringUtils
                        .changeTableName2CamelFirstUpper(tableName, "_")+"Bean";
				})
				.build(Resources.getResourceAsStream("config.properties"));
		generator.generate();
	}
}
```

## �Զ���ӳ������

```java
import java.io.IOException;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.type.JdbcType;

import com.github.zhuyizhuo.generator.mybatis.generator.Generator;
import com.github.zhuyizhuo.generator.mybatis.generator.GeneratorBuilder;

public class TestGenerator {
	
	public static void main(String[] args) throws IOException {
		/*
	     * �Զ������ݿ���java����ӳ��
	     * �������ݿ�����ΪNUMBER ������Ĭ��ӳ��ΪInteger ���Զ���ӳ�� ����������ָ��ΪString
	     * oracle ���ݿ����� TIMESTAMP Ĭ��ӳ��Ϊ java.util.Date �˴�����ӳ��Ϊjava.sql.Date
	     */
		Generator generator = new GeneratorBuilder()
				.addTypeMapper("NUMBER",JdbcType.VARCHAR,String.class)
				.addTypeMapper("TIMESTAMP", JdbcType.TIMESTAMP, java.sql.Date.class)
				.build(Resources.getResourceAsStream("config.properties"));
		generator.generate();
	}
}
```

## �Զ���������

> ���ó���: �����Ҫ���ݱ���Ϣ���ɸ������� ���� ����ҳ��/service/controller��  �ṩ����������չ����  �����ݿ���ʡ�ı�ṹ��װΪ���� ��������չ

```java
import java.io.IOException;
import java.util.List;

import org.apache.ibatis.io.Resources;

import com.github.zhuyizhuo.generator.mybatis.dto.JavaColumnInfo;
import com.github.zhuyizhuo.generator.mybatis.extension.service.GeneratorService;
import com.github.zhuyizhuo.generator.mybatis.generator.Generator;
import com.github.zhuyizhuo.generator.mybatis.generator.GeneratorBuilder;
import com.github.zhuyizhuo.generator.mybatis.vo.GenerateInfo;

public class TestGenerator {
    	public static void main(String[] args) throws IOException {
		Generator generator = new GeneratorBuilder().addGeneratorService(new GeneratorService() {
            //GenerateInfo Ϊ���ݿ���Ϣ�������� 
            //�ɽ��˶���תΪjson��ӡ�����鿴�ṹ �Լ�������Ҫ���л�ȡ�ֶ� �����Զ������ɸ�������
			@Override
			public void generate(GenerateInfo generateInfo) {
				System.out.println("tableName:" + generateInfo.getTableInfo().getTableName());
				List<JavaColumnInfo> columnLists = generateInfo.getTableInfo().getColumnLists();
				for (int i = 0; i < columnLists.size(); i++) {
					JavaColumnInfo javaColumnInfo = columnLists.get(i);
					System.out.println("\t private " + javaColumnInfo.getJavaDataType() + " " + javaColumnInfo.getJavaColumnName() + ";");
				}
			}
		}).build(Resources.getResourceAsStream("config.properties"));
		generator.generate();
	}
}

```

`java8` lambda ���ʽ

```java
public static void main(String[] args) throws IOException {
    Generator generator = new GeneratorBuilder()
        .addGeneratorService((generateInfo)->{
            System.out.println("tableName:" + generateInfo.getTableInfo().getTableName());
            List<JavaColumnInfo> columnLists = generateInfo.getTableInfo().getColumnLists();
            for (int i = 0; i < columnLists.size(); i++) {
                JavaColumnInfo javaColumnInfo = columnLists.get(i);
                System.out.println("\t private " + javaColumnInfo.getJavaDataType() + " " + javaColumnInfo.getJavaColumnName() + ";");
            }
        }).build(Resources.getResourceAsStream("config.properties"));
    generator.generate();
}
```

