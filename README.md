# Файл `tsconfig.json`:

- устанавливает корневой каталог проекта TypeScript;
- выполняет настройку параметров компиляции;
- устанавливает файлы проекта.


Присутствие файла `tsconfig.json` в папке указывает TypeScript, что это корневая папка проекта.

Внутри `tsconfig.json` указываются настройки компилятора TypeScript и корневые файлы проекта.

Программа компилятора `tsc` ищет файл `tsconfig.json` сначала в папке, где она расположена, затем поднимается выше и ищет в родительских папках согласно их вложенности друг в друга.

Команда `tsc --project C:\path\to\my\project\folder` берет файл `tsconfig.json` из папки, расположенной по данному пути.

Файл `tsconfig.json` может быть полностью пустым, тогда компилятор скомпилирует все файлы с настройками заданными по умолчанию.

Опции компилятора, перечисленные в командной строке перезаписывают собой опции, заданные в файле `tsconfig.json`.
```json
{
  // Загрузить другой конфигурационный файл `tsconfig.json`, взятый за основу, и перезаписать его значениями из секций ниже.	
  "extends": "./configs/base", 		
  
  // При значении true указывает используемой редактору кода производить компиляцию при каждом сохранении файлов TypeScript. Поддерживается не всеми редакторами кода.
  "compileOnSave": true,			
  
  // Настраивает параметры компиляции. Параметры называются также, как и в командной строке.
  "compilerOptions": {

    // Основные настройки и настройки путей для создания выходных файлов:
		
    // Определяет тип импорта кода в итоговом файле, прописанном в "outFile". Необходимо задавать при использовании опции "outFile".
    "module": "amd",
		
    // Имя единого итогового выходного файла, в который будут помещен код из всех найденных TypeScript-файлов.
    "outFile": "./build/bundle.js",
		
    // Поместить все скомпилированные файлы в данную папку, согласно их вложенности в исходниках. Если задана опция "outFile", то опция "outDir" будет проигнорирована.
    // Если "outFile" и "outDir" не заданы, то выходные файлы будут созданы рядом со своими исходниками.
    "outDir": "./build",
		
    // Настройки для поиска @types
    // По умолчанию все видимые в проекте пакеты "@types", расположенные в папках "node_modules" на всех уровнях вложенности, используются при компиляции.
    // Но, если указан массив "typeRoots", тогда при компиляции будут использованы только описания типов, найденные в папках, расположенных по перечисленным в нем путях.
    // При этом описания типов, находящихся в других папках использованы не будут.
    // Папки с пакетами описаний типов обычно содержат внутри себя файл "index.d.ts" или "package.json" со свойством "types".
    // При компиляции будут использованы только файлы описания типов ".d.ts" находящиеся в этой папке.
    "typeRoots" : [ 					
    	"./typings" 						
    ],
		
    // Если указан параметр "types", то из всех найденных будут использованы только те описания типов, что указаны в его массиве, а именно: "./typings/node", "./typings/lodash", "./typings/express".
    // Другие найденные типы использоваться не будут.
    // Задание "types": [] приведет к отключению автоматического использования описаний типов из папок "@types".
    "types" : ["node", "lodash", "express"],
		
    // Путь до папки с которой надо начинать поиск входных файлов. Обычно корневая директория вычисляется по списку входных файлов. Данная опция необходима для проверки, что все найденные TypeScript-файлы находятся внутри корневой папки.
    "rootDir": "../src",
		
    // Список корневых папок, совокупный контент которых представляет структуру проекта для компиляции.
    "rootDirs": [
      "src/views",
      "generated/templates/views"
    ],
		
    // Путь до базовой папки для поиска не относительных путей до файлов.
    "baseUrl": ".",
		
    // Укажите сопоставление маршрутов для вычисления по сравнению с параметром baseUrl.
    "paths": {
      "jquery": ["node_modules/jquery/dist/jquery"] // Путь относительно "baseUrl".
    },
		
    // Набор библиотечных файлов полифилов, которые будут включены в итоговый выходной файл.
    "lib": ["es5", "es6", "es2015.promise", "es2016.array.include"],
		
    // Тип кода создаваемого итогового файла.
    "target": "es3",
		
    // Включать ли поддержку ".tsx" файлов?
    "jsx": "react",
		
    // Укажите фабричную функцию JSX, чтобы использовать, когда таргетинг реагирует на обработку JSX, например: 'React.createElement' или 'h'. Требуется TypeScript версии 2.1 или новее.
    "jsxFactory": "React.createElement",
		
    // Разрешать компилировать файлы с JavaScript-кодом?
    "allowJs": false,
		
    // Сообщить об ошибках в .js-файлах? Используйте совместно с "allowJs".
    "checkJs": false,
		
    // Обеспечьте полную поддержку итераций для for - in, ..., деструктуризации при настройке на ES5 или ES3?
    "downlevelIteration": false,
		
    // Не создавать итоговый файл, если во время компиляции произошла ошибка.
    "noEmitOnError": true,
		
    // Не помещать в код итогового файла функции хелперы.
    "noEmitHelpers": false,
		
    // Имортировать созданные хелперы (__extends, __rest и так далее) из "tslib".
    "importHelpers": false,
		
    // Показывать ошибку, если где-то найдены неиспользуемые локальные значения.
    "noUnusedLocals": true,
		
    // Показывать ошибку, если где-то найдены неиспользуемые параметры.
    "noUnusedParameters": true,
		
    // Значения "null" и "undefined" могут быть присвоены только значениям данного типа и значениям только с типом "any"?
    "strictNullChecks": false,
		
    // Не записывать 'use strict' в итоговый выходной файл?
    "noImplicitUseStrict": false,
		
    // Компилировать ли каждый файл в строгом режиме и создавать ли 'use strict' для каждого выходного файла? Требуется TypeScript версии 2.1 или новее.
    "alwaysStrict": true,
		
    // Включить ли все строги проверки типов сразу: noImplicitAny, noImplicitThis, alwaysStrict, strictNullChecks, strictFunctionTypes, strictPropertyInitialization?
    "strict": false,
		
    // Удалить все комментарии из итогового файла.
    "removeComments": true,
		
    // Создавать ли соответствующие source map файлы ".map"?
    "sourceMap": true,
		
    // Окрашивать в терминале сообщения об ошибках.
    "pretty": true,
		
    // Запустить компилятор в режиме отслеживания изменений во входных файлах и их повторной компиляции?
    "watch": true,

    // Дополнительные настройки:
		
    // Кодировка входных файлов.
    "charset": "utf8",
		
    // Создавать ли соответствующие файлы ".d.ts"?
    "declaration": false,
		
    // Путь до папки, в которую будут записаны созданные соответствующие файлы ".d.ts".
    "declarationDir": ".",
		
    // Показывать ли диагностическую информацию?
    "diagnostics": false,
		
    // Записывать ли UTF-8 Byte Order Mark (BOM) в начало итогового файла?
    "emitBOM": false,
		
    // Помещать ли source map в итоговый файл, вместо того чтобы иметь отдельный файл с source map?
    "inlineSourceMap": false,
		
    // Помещать ли source в итоговый файл рядом с source map?
    "inlineSources": false,
		
    // Печатать ли имена файлов при компиляции?
    "listFiles": false,
		
    // Путь до папки, в которой дебаггер браузера должен будет искать файлы с source map.
    "mapRoot": ".",
		
    // Определяет тип завершения строк в итоговом файле.
    "newLine": "CRLF",
		
    // Не создавать итоговый файл.
    "noEmit": false,
		
    // Показывать ошибку, если где-то задан тип "any".
    "noImplicitAny": false,
		
    // Показывать ошибку на "this", если где-то задан тип "any".
    "noImplicitThis": false,
		
    // Не использовать стандартный библиотечный файл по умолчанию (lib.d.ts).
    "noLib": false,
		
    // Не добавлять "/// <reference path="..." />" в список скомпилированных файлов.
    "noResolve": false,
		
    // Отключить строгую проверку типов джинериков в типах функций?
    "noStrictGenericChecks": false,
		
    // Пропустить проверку типов из стандартной библиотеки по умолчанию?
    "skipDefaultLibCheck": false,
		
    // Не проверять типы, заданные во всех файлах описания типов (*.d.ts)?
    "skipLibCheck": false,
		
    // Не удалять объявления const enum из итогового файла.
    "preserveConstEnums": false,
		
    // Не заменять символические ссылки на их реальный путь, обрабатывать символический файл как реальный.
    "preserveSymlinks": false,
		
    // Обрабатывать каждый файл, как отдельный изолированный модуль.
    "isolatedModules": false,
		
    // Путь до папки, в которой дебаггер должен искать исходные source файлы.
    "sourceRoot": ".",
		
    // Подавлять избыточные проверки свойств для объектных литералов?
    "suppressExcessPropertyErrors": false,
		
    // Подавлять "noImplicitAny" ошибки для индексирования объектов, не имеющих индексных подписей.
    "suppressImplicitAnyIndexErrors": false,
		
    // Не создавать объявления для кода, который имеет аннотацию JSDoc /** @internal */.
    "stripInternal": false,
		
    // Включить экспериментальную поддержку декораторов EcmaScript?
    "experimentalDecorators": false,
		
    // Создавать метаданные для объявлений декораторов в исходном коде?
    "emitDecoratorMetadata": false,
		
    // Определить способ поиска модулей в папках: как в Node.js или классический, как в TypeScript 1.5 и ниже.
    "moduleResolution": "classic",
		
    // Не создавать сообщений об ошибках, если в коде найдены неиспользуемые метки label?
    "allowUnusedLabels": false,
		
    // Сообщить об ошибке, когда не все пути кода в функции возвращают значение?
    "noImplicitReturns": false,
		
    // Сообщить об ошибке в случае обнаружения проваливания в конструкции switch-case?
    "noFallthroughCasesInSwitch": false,
		
    // Сообщить об ошибке в случае обнаружения кода, который никогда не будет выполнен?
    "allowUnreachableCode": false,
		
    // Запретить несогласованные ссылки на один и тот же файл?
    "forceConsistentCasingInFileNames": false,
		
    // Список плагинов для сервера языка TypeScript для загрузки. Требуется TypeScript версии 2.3 или новее.
    "plugins": [],
		
    // Выводить в логи сообщения о нахождении путей до модулей.
    "traceResolution": false,
		
    // Разрешить импортировать модули не имеющие внутри себя "import default"?
    "allowSyntheticDefaultImports": false,
		
    // Печатать список всех выходных файлов при компиляции. Требуется TypeScript версии 2.0 или новее.
    "listEmittedFiles": false,
		
    // Отключить ограничение размера в проекте JavaScript.
    "disableSizeLimit": false,
		
    // Максимальная глубина поиска зависимостей внутри node_modules и загрузки файлов JavaScript. Применяется только вместе с заданной опцией "allowJs".
    "maxNodeModuleJsDepth": 0,
    
    // Отключить проверку бивариантных параметров для типов функций.
    "strictFunctionTypes": false,
    
    // Убедитесь, что свойства класса, имеющие значения undefined, получают новые значения внутри конструктора.
    "strictPropertyInitialization": false,
    
    // Создать хелперы __importStar и __importDefault для обеспечения совместимости с экосистемой Babel и включить allowSyntheticDefaultImports для совместимости с системой типов.
    "esModuleInterop": false,
  }
  
  // Список относительных или абсолютных путей до конкретных исходных файлов, которые обязательно надо скомпилировать.
  // Если секция "files" не указана, то компилятор по умолчанию включает все файлы с расширением *.ts и *.tsx, которые находятся в корневой папке и внутренних подпапках проекта.
  // Если секция "files" указана, то скомпилируются файлы, которые в ней перечислены.
  // Все файлы, на которые есть ссылки в файлах из секции "files", также скомпилируются.
  "files": [ 
    "core.ts",
    "app.ts"
  ],
  
  // Вместе с компиляцией только конкретных исходных файлов можно компилировать только файлы в заданных папках, которые будут найдены через регулярные выражения, которые принимают только следующие значения:
  // - букву или цифру;
  // - * - ноль или более любых символов, не включая разделители директорий "/" и "\";
  // - ? - один любой символ, не включая разделители директорий "/" и "\";
  // - **/ - рекурсивно включить любую подпапку.
  // Если путь до папки заканчивается так "*" или так ".*", тогда в ней будут скомплированы все файлы с расширениями .ts, .tsx, .d.ts, а также .js и .jsx, если опция "allowJs" будет равна true.
  
  // Секция "include" позволяет скомпилировать все файлы, находящиеся в заданных папках.
  // Если секция "files" и секция "include" заданы вместе, то будут скомпилированы только файлы, перечисленные в обеих секциях.
  // Все файлы, на которые есть ссылки во включенных файлах из секции "files" и секции "include", также скомпилируются.
  "include": [ 
    "src/**/*",
  ],
  
  // Секция "exclude" позволяет исключить при компиляции определенные файлы, которые находятся в заданных папках секции "include" или в папках всего проекта, если секция "include" не задана.
  // Компилятор не будет учитывать перечисленные в секции "exclude" файлы TypeScript, которые находятся в папках из секции "include".
  // Однако файлы, заданные в секции "files" будут обязательно скомпилированы.
  // Если секция "exclude" не указана, то по умолчанию будут исключаться из компиляции все файлы из папок:
  // - node_modules,
  // - bower_components,
  // - jspm_packages,
  // - файлы из папки, указанной в опции компилятора "outDir".
  "exclude": [
    "src/**/*.spec.ts",
    "node_modules"
  ]
}
```
