4. Add Swagger decorators in your controllers

Swagger only shows endpoints if you decorate them.

Example:

import { Controller, Get } from '@nestjs/common';
import { ApiTags, ApiOperation, ApiResponse } from '@nestjs/swagger';

@ApiTags('cats')
@Controller('cats')
export class CatsController {

@Get()
@ApiOperation({ summary: 'Get all cats' })
@ApiResponse({ status: 200, description: 'List of cats' })
findAll() {
return [];
}
} 5. Add DTO documentation (important)

Swagger becomes powerful when you document DTOs:

import { ApiProperty } from '@nestjs/swagger';

export class CreateCatDto {
@ApiProperty({ example: 'Tom' })
name: string;

@ApiProperty({ example: 3 })
age: number;
} 6. Optional: Better Swagger setup (recommended)
const config = new DocumentBuilder()
.setTitle('My API')
.setDescription('API documentation')
.setVersion('1.0')
.addBearerAuth() // if using JWT
.build();

const document = SwaggerModule.createDocument(app, config, {
deepScanRoutes: true,
});
